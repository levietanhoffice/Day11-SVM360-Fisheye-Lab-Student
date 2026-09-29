# Äá» xuáº¥t gold set theo camera â€” tÃ¬nh huá»‘ng giáº£ láº­p

**Äáº§u bÃ i:** 50.000 frame tá»« bá»‘n camera SVM, ngÃ¢n sÃ¡ch chá»n 200 frame Ä‘á»ƒ review/gold. ÄÃ¢y lÃ  tÃ¬nh huá»‘ng trÃªn slide,
**khÃ´ng pháº£i** 50.000 frame cÃ³ trong repo. PhÃ¢n bá»• Ä‘Ãºng 200 á»Ÿ `45_sampling_plan.csv` cho bá»‘n camera, má»—i camera cÃ³
normal vÃ  hard slice. â€œGold setâ€ á»Ÿ Ä‘Ã¢y lÃ  **káº¿ hoáº¡ch táº¡o** reference sau kiá»ƒm chá»©ng, khÃ´ng pháº£i teaching reference
ADASIND hoáº·c nhÃ£n báº¡n vá»«a váº½. Náº¿u cáº§n, dÃ¹ng `notebooks/day11-svm360-colab.ipynb` Ä‘á»ƒ thá»­ tá»•ng phÃ¢n bá»•; notebook
khÃ´ng lÃ m thay pháº§n lÃ½ do.

| camera_id | Hard case cáº§n chá»n | VÃ¬ sao dá»… sai | Annotation space / calibration cáº§n giá»¯ | CÃ¡ch review trÆ°á»›c khi gá»i lÃ  gold |
|---|---|---|---|---|
| front | Káº¹t xe (nhiá»u xe), ngÆ°á»£c sÃ¡ng chÃ³i náº¯ng | Váº­t thá»ƒ chá»“ng láº¥p (occlusion) máº¡nh, Ã¡nh sÃ¡ng lÃ m trÆ°á»£t mÃ©p xe. | R01 (H=40), mÃ©p lens_border, ego_body (náº¯p capo). | Äá»‘i chiáº¿u chÃ©o 2 ngÆ°á»i (Blind QA) vÃ  kiá»ƒm tra chuá»—i frame liÃªn tiáº¿p (temporal). |
| rear | Äi Ä‘Ãªm bá»‹ Ä‘Ã¨n pha chiáº¿u tháº³ng, xe sÃ¡t Ä‘uÃ´i | LÃ³a sÃ¡ng máº¥t chi tiáº¿t bÃ¡nh xe, mÃ©p dÆ°á»›i xe bá»‹ che khuáº¥t. | Focus vÃ o Ä‘iá»ƒm tiáº¿p xÃºc bÃ¡nh xe, ranh giá»›i bÃ³ng Ä‘á»• vÃ  nguá»“n sÃ¡ng. | Review cÃ³ Ä‘á»‘i chiáº¿u Ä‘á»™ sÃ¡ng tÆ°Æ¡ng pháº£n vÃ  tháº£o luáº­n Ä‘á»“ng thuáº­n (consensus). |
| left | Xe mÃ¡y táº¡t ngang nhanh, Ä‘iá»ƒm mÃ¹ hÃ´ng xe | Äá»™ mÃ©o fisheye cá»±c Ä‘áº¡i á»Ÿ vÃ¹ng rÃ¬a (edge) khiáº¿n váº­t thá»ƒ cong váº¹o. | BÃ¡m mÃ©p cong Ä‘iá»ƒm cá»±c Ä‘áº¡i (trÃ¡nh BOX_GEOMETRY sai), váº½ ego_body bÃªn hÃ´ng. | DÃ¹ng cÃ´ng cá»¥ overlay Ä‘á»‘i chiáº¿u, Ä‘o IoU kháº¯t khe á»Ÿ rÃ¬a áº£nh. |
| right | Xe mÃ¡y cáº·p lá» pháº£i, khu vá»±c gÃ³c cháº¿t | MÃ©o quang há»c máº¡nh, xe mÃ¡y dá»… bá»‹ xÃ© hÃ¬nh. | ChÃº trá»ng bounding box hÃ¬nh cung, xá»­ lÃ½ mÃ©p lens_border. | PhÃ¢n tÃ­ch chÃ©o bá»Ÿi AI team vÃ  chuyÃªn gia (Super-QC) Ä‘á»ƒ chá»‘t chuáº©n. |

- Khi nÃ o cáº§n refresh gold set (Ä‘á»•i camera, calibration hoáº·c rule): Khi cÃ³ sá»± thay Ä‘á»•i vá» pháº§n cá»©ng (Ä‘á»•i loáº¡i tháº¥u kÃ­nh, gÃ³c nghiÃªng camera/calibration má»›i) hoáº·c khi cáº­p nháº­t bá»™ quy táº¯c (rule version má»›i) lÃ m thay Ä‘á»•i cÃ¡ch Ä‘á»‹nh nghÄ©a class/bounding box.
- Má»™t ca seam/cross-camera cáº§n policy vÃ  evidence trÆ°á»›c khi ghÃ©p hai box: Cáº§n quy Ä‘á»‹nh (policy) rÃµ rÃ ng viá»‡c tÃ­nh Ä‘iá»ƒm IoU/ghÃ©p box khi váº­t thá»ƒ bá»‹ chia lÃ m Ä‘Ã´i á»Ÿ 2 camera liá»n ká» (vÃ­ dá»¥ gÃ³c front vÃ  right). Báº±ng chá»©ng (evidence) lÃ  áº£nh Ä‘á»“ng bá»™ timestamp (cÃ¹ng má»™t mili-giÃ¢y) tá»« cáº£ 2 camera Ä‘á»ƒ Ä‘á»‘i chiáº¿u.
- VÃ¬ sao peer agreement hoáº·c quality report trÃªn áº£nh má»™t camera chÆ°a chá»©ng minh gold set Ä‘Ãºng cho cáº£ bá»‘n camera: Tá»· lá»‡ Ä‘á»“ng thuáº­n (agreement) cao á»Ÿ má»™t camera (vÃ­ dá»¥ front - Ã­t mÃ©o) khÃ´ng thá»ƒ Ä‘áº¡i diá»‡n cho cÃ¡c camera khÃ¡c (left/right - mÃ©o fisheye ráº¥t máº¡nh). Má»—i gÃ³c mÃ¡y cÃ³ má»™t phÃ¢n phá»‘i lá»—i hoÃ n toÃ n khÃ¡c nhau, vÃ  chÆ°a giáº£i quyáº¿t Ä‘Æ°á»£c bÃ i toÃ¡n chá»“ng láº¥p á»Ÿ vÃ¹ng ghÃ©p ná»‘i (seam) giá»¯a cÃ¡c camera.
