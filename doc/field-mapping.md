# 字段映射 Field Mapping — Intake Form + Consent to Osteopathic Treatment

> 来源：`Intake-form.pdf`（Health History Form）+ `CONSENT-TO-OSTEOAPTHIC-TREATMENT.pdf`
> 日期：2026-10-06

---

## 表一：Health History Form（初诊表）

### A. 基本信息 Patient demographics
| 字段 | 类型 | 备注 |
|---|---|---|
| full_name | text, 必填 | |
| phone | tel, 必填 | |
| address | text, 必填 | |
| occupation | text | |
| date_of_birth | date, 必填 | |

### B. 就诊史 History
| 字段 | 类型 | 备注 |
|---|---|---|
| received_massage_before | yes/no | 纸质写的是 massage therapy，原样保留 |
| referred_by_practitioner | yes/no | |
| referral_name_address | text | referred=yes 时显示 |

### C. 病史勾选 Conditions（多选 checkbox 组）
**Cardiovascular**（多选）: high_blood_pressure / low_blood_pressure / chronic_congestive_heart_failure / heart_attack / phlebitis_varicose_veins / stroke_cva / pacemaker_or_similar_device / heart_disease
- family_history_cv: yes/no

**Respiratory**（多选）: chronic_cough / shortness_of_breath / bronchitis / asthma / emphysema
- family_history_resp: yes/no

**Infections**（多选）: hepatitis / skin_conditions / tb / hiv / herpes

**Other conditions**:
| 字段 | 类型 |
|---|---|
| loss_of_sensation_where | text（"where?"） |
| diabetes_onset | text（"onset"） |
| allergies_to_what | text（"to what?"） |
| allergy_reaction_type | text（"type of reaction"） |
| epilepsy | checkbox |
| cancer_where | text（"where?"） |
| skin_conditions_what | text（"what?"） |
| arthritis | checkbox |
| family_history_arthritis | yes/no |

**Head/Neck**（多选）: headaches / migraines / vision_problems / vision_loss / ear_problems / hearing_loss

**Women**:
| 字段 | 类型 |
|---|---|
| pregnant | yes/no |
| pregnant_due | date（"due:"，pregnant=yes 时显示） |
| gyn_conditions_what | text（"what?"） |

| general_health | text | "Overall, how is your general health?" |

### D. 家庭医生 Primary care physician
| pcp_name | text |
| pcp_address | text |

### E. 用药 Current medications
| current_medications | textarea |
| medication_treats | text（"it treats:"） |

### F. 其他疾病 Other medical conditions
| other_medical_conditions | yes/no |
| other_medical_conditions_what | text（yes 时显示；例：digestive conditions, haemophilia, osteoporosis, mental illness） |

### G. 是否同时接受其他治疗 Concurrent care
| receiving_other_treatment | yes/no |
| other_treatment_for_what | textarea（yes 时显示） |

### H. 体内植入物 Implants / equipment
| has_implants | yes/no（pins, wires, artificial joints, special equipment） |
| implants_what | text（"what?"） |
| implants_where | text（"where?"） |

### I. 本次就诊原因 Reason for visit
| reason_for_visit | textarea（含"location of any tissue or joint discomfort"） |
| surgery_date | date |
| surgery_nature | text |
| injury_date | date |
| injury_nature | text |

### J. 诊所填写（患者端不填） Clinic-side only
- initial_health_history_date（初诊日期）
- update_1 … update_4（复诊更新日期）
- notes（备注栏）

---

## 表二：Consent to Osteopathic Treatment（治疗知情同意书）

### 固定法律文本（网页与 PDF 必须逐字呈现）
- 风险告知 ×4：slight pain/sourness/numbness/heaviness；dizziness/nausea（hungry or tired 时）；skin bruise（~1周消退）；soft tissue swelling/sourness（次日）
- 确认讨论 ×4：condition / nature of treatment / risks and benefits / alternatives
- 理解声明 ×4：可穿衣或裸体治疗（draping 遮盖）；可随时叫停；已获得提问机会；female adult assistant 全程在场监督

### 可填字段
| 字段 | 类型 | 备注 |
|---|---|---|
| therapist_name | text, 必填 | "offered to me by ___" |
| treatment_areas | 多选 | head_neck / face_mouth / back_upper_mid_lower / shoulder_arm / elbow_wrist_hand / stomach / knees / ankle_feet / leg / others |
| treatment_areas_other_text | text | others 勾选时显示 |
| consent_scope_with | text, 必填 | "all my present and future care with ___" |
| signature | 手写签名图, 必填 | canvas 签名板 |
| signed_as | patient / legal_guardian | 纸质 "(or Legal Guardian)" |
| signature_date | 自动 | 提交时间 |

---

## 设计要点

1. **PHIPA**：这是健康信息（health information），安省 PHIPA 适用。存储必须加密（at rest）、访问控制、audit log。**存健康数据前建议先过一遍 legal review**（和 Groway med-aesthetics 模块同样的要求）。
2. **PDF 即证据**：提交瞬间生成 PDF 并冻结存档（immutable），同时存 SHA-256 hash。稽查时调 PDF 即是"当时签的版本"，避免"数据库里的数据和纸质对不上"的质疑。
3. **知情同意书的法律文本逐字呈现**：网页和 PDF 都要完整显示 risks/acknowledgements/understandings 全文，不能只存勾选结果——insurer 查的就是"你有没有告知风险"。
4. **签名场景决定实现**：店里当面签（平板，简单）vs 远程签（要身份验证链接，复杂一个量级）。
5. **Typo 待确认**：原文件标题 "CONSENT TO OSTEOAPTHIC TREATMENT" 拼错（应为 OSTEOPATHIC）。电子版改不改？建议改，但先确认——insurer 可能拿着原文件逐字比对。

## 待确认事项
- [ ] 这是谁的诊所？（partner 的店？还是别的客户？）
- [ ] 保险公司是否接受自生成的 PDF 电子版？（最关键，不接受就白做）
- [ ] 签名场景：在店里当面签，还是发链接远程签？
- [ ] 部署位置：本地 IIS / 公网服务器？
- [ ] "OSTEOAPTHIC" typo 电子版是否修正？
- [ ] J 部分（诊所填写的复诊更新日期）要不要也进系统，还是只做患者填写部分？