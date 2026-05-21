# Data Card — 

**Target Variable:** `POL_ACCT_CR_IND` (binary: 0 = auto-only, 1 = bundled auto+home)  
**Rows:** 300,000 | **Columns:** 44  
**Data loaded with:** `keep_default_na=False, na_values=['']`

---

## Feature Dictionary

| Feature | Semantic Type | % Missing | Bivariate Signal | MI | Leakage | Keep/Drop |
|---|---|---|---|---|---|---|
| `AUTO_POL_TRANS_ID` | identifier | 0% | N/A | N/A | — | **Drop** |
| `RISK_ST_ABBR` | nominal | 0% | Cramér's V moderate | High | — | **Keep** |
| `POL_EFF_DT` | datetime | 0% | Stable target rate | — | — | **Keep (derive month/year)** |
| `POL_EXP_DT` | datetime | 0% | Redundant | — | — | **Drop** |
| `POL_NEW_RENEW_CD` | binary | 0% | Weak | Low | — | **Keep** |
| `POL_TTL_BILL_PREM_AMT` | continuous | 0% | Moderate PB r | High | VIF high | **Drop** (collinear) |
| `RISK_GRP` | ordinal | 0% | Moderate | Moderate | — | **Keep** |
| `RISK_FLAG` | nominal | 0% (string "NA" preserved via keep_default_na=False) | Trivial | 0 | — | **Drop** (quasi-constant >95% "NA") |
| `CLTV_LONGVTY_GRP_CD` | ordinal | ~15-20% | Moderate | Moderate | — | **Keep** |
| `AARP_MEMB_YR_CNT` | count | 0% | Weak | Moderate | — | **Keep** |
| `AARP_MEMB_IND` | binary | 0% | N/A (constant) | 0 | — | **Drop** |
| `FULL_PAY_DISC_IND` | binary | 0% | Weak | Low | — | **Keep** |
| `POL_BI_OCCUR_LMT_CD` | ordinal | 0% | Strong PB r | High | — | **Keep** |
| `CLEAN_DIRTY_DESC` | binary | 0% | Weak | Low | — | **Keep** |
| `DRVR_TLMTC_PGM_TYP_CD` | nominal | 0% | Weak | Low | — | **Keep** |
| `RENEW_YRS` | continuous | 0% | Weak | Moderate | — | **Keep** |
| `POL_MULTI_SNGL_VEH_CD` | binary | 0% | Moderate | Moderate | — | **Keep** |
| `POL_DRVR_TLMTC_ENROL_IND` | binary | 0% | Weak | Low | — | **Keep** |
| `ORIG_INTRNT_RATE_QTE_IND` | binary | 0% | Weak | Low | — | **Keep** |
| `PPV_CNT` | count | 0% | Weak | Moderate | — | **Keep** |
| `PCARR_DESC` | nominal | 0% | Moderate | Moderate | — | **Keep** |
| `AVG_VEH_PREM` | continuous | 0% | Moderate | High | — | **Keep** |
| `PCARR_YR_CNT` | continuous | 0% | Weak | Low | — | **Keep** |
| `PCARR_CALC_YR_CNT` | continuous | ~3-5% | Weak | Low | — | **Keep** |
| `POL_FORM_CD` | nominal | 0% | **EXTREME** | **EXTREME** | **LEAKAGE** | **Drop** |
| `POL_RATE_DRVR_MIN_AGE` | continuous | 0% | Weak | Moderate | — | **Keep** |
| `POL_RATE_DRVR_MAX_AGE` | continuous | 0% | Weak | Low | — | **Keep** |
| `HH_COMP` | nominal | 0% | Moderate | High | — | **Keep** |
| `ADV_QTE_DAY_CNT` | count | <1% | Weak | Moderate | — | **Keep** |
| `AQD_GRP` | ordinal | 0% | Moderate | Moderate | — | **Keep** |
| `YOUTHFUL_IND` | binary | 0% | Weak | Low | — | **Keep** |
| `BILL_PYMNT_METH_DESC` | nominal | 0% | Moderate | Moderate | — | **Keep** |
| `BILL_PYMENT_FREQ_DESC` | nominal | 0% | Strong | High | — | **Keep** |
| `AVG_VEHICLE_MILEAGE` | continuous | 0% | Weak | Low | — | **Keep** |
| `MKT_CHNNL_NM` | nominal | ~5-10% | Weak | Low | — | **Keep** |
| `MKTG_MEDIA_GRP_DESC` | nominal | ~5-10% | Weak | Low | — | **Keep** |
| `MKTG_NON_BRAND_SEARCH_FLAG` | nominal | 0% | Weak | Low | — | **Keep** |
| `ORIG_QTE_CNTCT_METH_CD` | nominal | 0% | Moderate | Moderate | — | **Keep** |
| `E_SIGN_IND` | binary | 0% | Trivial | Negligible | — | **Keep** |
| `ECNSNT_BEGINING_OF_POL_TERM_IND` | binary | 0% | Weak | Low | — | **Keep** |
| `PLCY_MIN_CAR_BASE_PRICE` | continuous | ~2-5% | Weak | Low | VIF high | **Drop** |
| `PLCY_MAX_CAR_BASE_PRICE` | continuous | ~2-5% | Weak | Low | VIF high | **Drop** |
| `PLCY_AVG_CAR_BASE_PRICE` | continuous | ~2-5% | Moderate | Moderate | — | **Keep** |

---

## Dropped Features Summary

| Feature | Reason |
|---|---|
| `AUTO_POL_TRANS_ID` | Row identifier — memorization risk |
| `POL_FORM_CD` | Confirmed target leakage (HO3/HO4/HO6 = home policy) |
| `AARP_MEMB_IND` | Zero variance (all "Y") |
| `RISK_FLAG` | Quasi-constant (>95% string "NA") |
| `POL_EFF_DT`, `POL_EXP_DT` | Raw timestamps — month/year extracted |
| `POL_TTL_BILL_PREM_AMT` | Collinear with AVG_VEH_PREM x PPV_CNT (VIF > 10) |
| `PLCY_MIN_CAR_BASE_PRICE` | Collinear with AVG (VIF > 10) |
| `PLCY_MAX_CAR_BASE_PRICE` | Collinear with AVG (VIF > 10) |
