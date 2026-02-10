
# Functional Specification

## Object Details
- **Include Name:** ZLOG_RATE_UPLOAD_E_P_CLS
- **Change Type:** Enhancement

## Business Requirement
A configurable logic is required during Rate Upload processing to modify the value passed to BDC field **Y_CHAR_VAL** based on configuration maintained in **ZLOG_EXEC_VAR**.

## Configuration
**Table:** ZLOG_EXEC_VAR  
- NAME = ZLOG_INCENTIVE_VAR_CHNGE  
- ACTIVE = X  
- REMARKS = Incentive Identifier

## Functional Logic
1. Fetch entries from ZLOG_EXEC_VAR where NAME = `ZLOG_INCENTIVE_VAR_CHNGE` and ACTIVE = `X`.
2. Compare ZLOG_EXEC_VAR-REMARKS with `<lfs_scl_itab>-SCAID`.
3. If matched, concatenate:
   - lw_scaval_9 and `<lfs_catyp>` separated by space.
4. If not matched, existing logic continues.

## Program Change
- Apply logic before:
  `PERFORM bdc_field USING 'Y_CHAR_VAL' lw_scaval_9.`
- Reference Line: 4624

## Testing Scenarios
- Match found → Value concatenated
- No match / Inactive config → Existing logic

## Notes
- No impact if configuration inactive.
- Backward compatible.
