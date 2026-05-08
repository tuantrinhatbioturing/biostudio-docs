# BioStudio AI Prototype - Questions & Answers

Date: 2026-05-08
Context: Interactive prototype development for BioStudio AI product direction inspired by bio.xyz chat

---

## Q1: Nội dung ở Tab Data ở Right panel là gì?

### Trả lời:

Tab **Data** ở Right Panel (bảng thông tin bên phải) gồm **3 phần chính**:

### 1. Dataset
Thông tin cơ bản về tập dữ liệu đang phân tích:

| Thuộc tính | Giá trị |
|---|---|
| **Modality** | Single-cell RNA-seq (10x Genomics) |
| **Cells** | 12,847 tế bào |
| **Genes** | 33,694 gene |
| **Samples** | 4 bệnh nhân |
| **Groups** | 2 responders, 2 non-responders |
| **Platform** | 10x Genomics Chromium v3 |

### 2. Metadata Quality
Đánh giá chất lượng metadata bằng thanh tiến trình (% hoàn thành):

| Metadata | Quality |
|---|---|
| Sample IDs | 100% |
| Treatment status | 100% |
| Response labels | 100% |
| Batch IDs | 50% (thiếu cho 3 samples) |
| Clinical metadata | 75% |
| Cell type labels | 0% (chưa có - cần annotation) |

### 3. Uploaded Files
Danh sách file đã upload:

| File | Kích thước |
|---|---|
| `melanoma_scRNAseq.h5ad` | 2.4 GB |
| `sample_metadata.xlsx` | 45 KB |
| `patient_clinical_data.csv` | 12 KB |

**Ý nghĩa trong workflow:** Tab Data xuất hiện ở **Bước 1** của AI workflow (sau khi hệ thống "Ingesting dataset metadata"). Nó giúp nhà khoa học biết AI đã hiểu đúng loại dữ liệu chưa, metadata có đủ chất lượng không, và file nào đã sẵn sàng.

---

## Q2: Ở mục Dataset, Modality là gì và có những loại nào?

### Trả lời:

## Modality là gì?

**Modality** (phương thức đo lường) trong sinh học -omics là **loại kỹ thuật giải trình tự được sử dụng để tạo ra dữ liệu**. Nó cho biết:
- **Độ phân giải** của dữ liệu: sample level, single-cell level, hay tissue location level?
- **Loại phân tử** được đo: RNA, protein, DNA, hay kết hợp?
- **Nền tảng công nghệ**: 10x Genomics, Illumina, Visium, ...

## Các loại Modality trong Prototype

Prototype hỗ trợ 4 loại chính:

| Modality | Tên đầy đủ | Độ phân giải | Mô tả |
|---|---|---|---|
| **scRNA-seq** | Single-cell RNA sequencing | **Tế bào đơn lẻ** | Đo biểu hiện gen ở từng tế bào riêng biệt. Dùng để phát hiện dị bào (tế bào CD8+ kiệt sức), annotation, trajectory. |
| **Bulk RNA-seq** | Bulk RNA sequencing | **Mẫu mô/tổng hợp** | Đo biểu hiện trung bình của toàn bộ mẫu. Dùng cho DEG, pathway enrichment giữa các nhóm điều trị. |
| **Spatial transcriptomics** | Spatial transcriptomics | **Vị trí không gian** | Giữ thông tin vị trí tế bào trong mô (tumor core, margin, stroma). Dùng cho neighborhood analysis. |
| **Multi-omics** | Multi-omics integration | **Đa lớp** | Kết hợp nhiều loại dữ liệu: transcriptomics + proteomics + epigenomics cùng lúc. |

## Tại sao Modality quan trọng?

Khi AI nhận câu hỏi: *"What cell populations drive resistance?"*, nó cần biết Modality để:
1. **Chọn đúng công cụ**: scRNA-seq → BBrowserX Pro; Spatial → SpatialX; Bulk → SmartBulk
2. **Hiểu đúng đơn vị phán tích**: cell level vs sample level vs spatial spot level
3. **Áp dụng đúng thuật toán**: Leiden clustering cho scRNA-seq, GSEA cho Bulk, Moran's I cho Spatial

---

## Q3: Dataset detected: single-cell RNA-seq (10x Genomics) xuất hiện ở đâu?

### Trả lời:

Nội dung này xuất hiện trong **AI chat** khi người dùng upload dữ liệu và hỏi "What cell populations drive resistance?". Cụ thể:

- **Vị trí:** `app/data/mockData.ts` → `chatMessages['rt-1']` → message `msg-3`
- **Vai trò:** AI tự động detect loại dữ liệu sau khi ingest
- **Nội dung:**
  - Dataset detected: single-cell RNA-seq (10x Genomics)
  - Samples: 12,847 cells from 4 patients
  - Groups: 2 responders, 2 non-responders

Đây là **Bước 1** trong AI workflow: *Question → Data understanding → Literature search → ...*

---

## Kiến trúc Prototype Layout

### Default View (AI Research)
| Panel | Nội dung |
|---|---|
| **Left** | Sidebar: Workspace, Research Threads, Projects, Navigation |
| **Center** | AI Chat + Kết quả phân tích (UMAP, biểu đồ, bảng DEG) |
| **Right** | Research State Panel (8 tabs: Overview, Data, Literature, Analysis, Evidence, Prediction, Report, Next Steps) |

### Notebook Editor View
- Chỉ mở khi click **Project → Notebook card**
- Layout: Left sidebar → Center Jupyter Notebook → Right AI Assistant Panel (8 tabs)

---

## 8 Tabs của Research State Panel (Right Panel)

| Tab | Nội dung |
|---|---|
| **Overview** | Objective, Hypothesis, Conclusion, Confidence Score |
| **Data** | Dataset info, Metadata Quality, Uploaded Files |
| **Literature** | Papers hỗ trợ với Relevance Score (vd: 95%) |
| **Analysis** | Methods, Parameters, Findings |
| **Evidence** | Cells/Clusters, Genes, Pathways, Cohorts, Notebook Outputs |
| **Prediction** | Predictions với Confidence, Evidence, Caveats |
| **Report** | Auto-generated manuscript + Export MD/DOCX |
| **Next Steps** | Recommended actions với Priority (High/Medium/Low) |

## Q4: Tab Overview có những gì? Objective, Hypothesis, Confidence là gì?

### Trả lời:

Tab **Overview** là tab quan trọng nhất — giống như **"tóm tắt luận án"** trong 5 giây.

#### Objective (Mục tiêu)
Câu hỏi gốc mà nhà khoa học đặt ra. AI tự động trích xuất từ câu hỏi người dùng. Giúp kiểm tra xem **AI có hiểu đúng vấn đề** không. Ví dụ: "Identify cell populations and molecular signatures associated with anti-PD-1 resistance..."

#### Hypothesis (Giả thuyết)
Giả thuyết AI đưa ra sau khi phân tích dữ liệu và tra Talk2Data. Không phải kết luận cuối cùng, mà là **"con đường AI đang đi"** để chứng minh. Ví dụ: "Exhausted CD8+ T cells and macrophage inflammatory signaling create an immunosuppressive microenvironment..."

#### Current Conclusion (Kết luận hiện tại)
Kết quả thực tế sau khi AI chạy pipeline. Hiển thị số liệu cụ thể. Ví dụ: "Non-responder samples show 2.3× more exhausted CD8+ T cells (42% vs 18%)..."

#### Confidence (Độ tin cậy)
Con số 0.0 - 1.0. Phân loại:
- **< 0.6:** Thấp → Cần thêm dữ liệu
- **0.6 - 0.8:** Trung bình → Cần validation
- **> 0.8:** Cao → Có thể tin tưởng viết paper
Kèm theo **Caveat** (hạn chế): Ví dụ "Limited to 4 patients. Cross-validation needed."
→ Đây là điểm khác biệt so với chatbot thông thường: AI **thừa nhận giới hạn** của nó.

#### Novelty Statement (Tính mới)
"Nghiên cứu này có gì mới so với thế giới?" AI so sánh với Talk2Data để xác định điểm độc đáo. Hữu ích khi viết abstract hoặc grant proposal.

---

## Q5: Tab Literature hiển thị gì? Relevance Score là gì?

### Trả lời:

Tab Literature hiển thị các **bài báo khoa học đã xuất bản** liên quan đến chủ đề nghiên cứu.

| Paper | Tác giả | Năm | Tạp chí | Relevance |
|---|---|---|---|---|
| Single-cell profiling reveals immune suppression... | Jerby-Arnon et al. | 2018 | Cell | **95%** |
| T cell exhaustion in cancer... | Thommen & Schumacher | 2018 | Nature Reviews Cancer | **92%** |
| Macrophage-mediated immune suppression... | DeNardo & Ruffell | 2019 | Cancer Immunology Research | **88%** |

#### Relevance Score (%)
AI đánh giá mức độ liên quan của từng bài báo đến kết quả hiện tại:
- **90-100%:** Cực kỳ liên quan
- **70-89%:** Liên quan
- **< 70%:** Tham khảo thêm

#### Ý nghĩa:
- Ngăn AI bịa đặt (hallucination). Mỗi kết luận đều phải có **nguồn gốc rõ ràng**.
- Xuất hiện ở **Bước 2** của workflow: AI search Talk2Data và PubMed sau khi hiểu dữ liệu.

---

## Q6: Tab Analysis có gì? Parameters là gì?

### Trả lời:

Tab Analysis liệt kê chi tiết các **phương pháp phân tích** đã chạy, tham số, và kết quả. Đây là phần **Methods** của nghiên cứu.

#### Ví dụ: Cell type annotation
- **Method:** SingleR + marker-based manual curation
- **Parameters:** reference=HumanPrimaryCellAtlas, n_markers=98
- **Findings:** 12 cell types; CD8+ T cells 34.2%, Macrophages 18.7%...

#### Ví dụ: Differential Expression
- **Method:** Wilcoxon rank-sum (Scanpy)
- **Parameters:** min_pct=0.25, logfc_threshold=0.25, pval_cutoff=0.05
- **Findings:** 1,247 DEGs; PDCD1/HAVCR2/LAG3 upregulated

#### Parameters (Tham số) là gì?
Là các giá trị cài đặt của thuật toán. Ví dụ:
- **resolution=0.8** trong Leiden clustering → clustering có tinh hay thô?
- **n_top_genes=2000** → chọn bao nhiêu gene biến đổi nhiều nhất?
- Người dùng có thể kiểm tra tham số có hợp lý không và điều chỉnh lại.

#### Ý nghĩa:
- **Transparency:** Kiểm tra AI làm đúng chưa
- **Reproducibility:** Người khác có thể replicate
- **Best-practice check:** So sánh với workflow chuẩn BioTuring

---

## Q7: Tab Evidence là gì? Tại sao cần?

### Trả lời:

Tab Evidence liên kết tất cả các **entities** (tế bào, gene, pathway, cohort) và **outputs** (biểu đồ, bảng) thành **chuỗi bằng chứng** hỗ trợ kết luận.

Mỗi kết luận AI đưa ra đều có thể **truy ngược** về bằng chứng gốc.

#### 5 nhóm Evidence:

**Cells / Clusters**
| Entity | Mô tả | Confidence |
|---|---|---|
| CD8+ T cells (Cluster 7) | Exhausted, PDCD1+/HAVCR2+/LAG3+ | **89%** |
| Macrophages (Cluster 4) | M2-like, CCL2+/CCL3+/MRC1+ | **84%** |

**Genes / Markers**
| Gene | Mô tả | Giá trị |
|---|---|---|
| PDCD1 (PD-1) | Exhaustion marker, log2FC=3.42 | Up in NR |
| HAVCR2 (TIM-3) | Exhaustion marker, log2FC=2.89 | Up in NR |

**Pathways**
- T cell exhaustion: GSEA NES=2.34, FDR=0.0012
- PD-L1 expression: GSEA NES=2.13, FDR=0.0034

**Cohorts**
- GSE123813: Anti-PD-1 non-responders, Jaccard similarity=0.62
- GSE145286: Anti-PD-1 non-responders, Jaccard similarity=0.67

**Notebook Outputs**
- UMAP plot (cell 6)
- Composition bar chart (cell 8)
- DEG table (cell 9)

#### Ý nghĩa:
- **Audit trail:** Reviewer kiểm tra từng bước
- **Connected ecosystem:** Liên kết cell → gene → pathway → cohort → output
- Phù hợp với **Section 5** của product ideation: "Ask BioTuring Data Inside Every Result"

---

## Q8: Tab Prediction là gì? Confidence khác gì so với Overview?

### Trả lời:

Tab Prediction là nơi AI **dự đoán ý nghĩa sinh học** — không chỉ mô tả dữ liệu mà còn đưa ra giải thích dựa trên curated references.

#### Các dự đoán trong prototype:

**1. Cell State Prediction**
- Prediction: High exhausted CD8 T-cell signature in non-responders
- Confidence: **89%**
- Evidence: PDCD1, HAVCR2, LAG3 upregulated
- Caveats: Limited to 4 patients; Single timepoint

**2. Phenotype Prediction**
- Prediction: Immune-resistant phenotype (cold tumor conversion)
- Confidence: **72%**
- Evidence: M2 macrophages 28% vs 12%
- Caveats: Needs cross-validation

**3. Similar Cohort**
- Prediction: Closest match GSE145286
- Confidence: **78%**
- Evidence: Jaccard similarity=0.67

#### Confidence ở Prediction khác gì Confidence ở Overview?

| | Overview Confidence | Prediction Confidence |
|---|---|---|
| **Ý nghĩa** | Tổng độ tin cậy của toàn bộ nghiên cứu | Độ tin cậy của từng dự đoán cụ thể |
| **Ví dụ** | "Nghiên cứu này đáng tin 72%" | "Dự đoán exhausted CD8+ đúng 89%" |
| **Cấu trúc** | 1 score cho cả project | Nhiều score cho từng prediction |

Mỗi prediction có:
- **Evidence** (bằng chứng): Dữ liệu hỗ trợ
- **Caveats** (hạn chế): Giới hạn cần lưu ý
- **Recommended validation:** Cách xác minh tiếp theo

#### Ý nghĩa:
- Điểm mạnh độc đáo của BioStudio AI so với chatbot
- Giúp tạo **hypothesis mới**
- Tránh **over-interpretation** nhờ caveats

---

## Q9: Tab Report tạo ra gì?

### Trả lời:

Tab Report tự động tạo **bản thảo manuscript-ready** từ toàn bộ nghiên cứu (MVP 5: Publication Copilot).

#### Nội dung mẫu:
```
OBJECTIVE
Identify cell populations and molecular signatures associated with anti-PD-1 
resistance in melanoma using single-cell transcriptomics.

METHODS
Single-cell RNA-seq analysis was performed on 12,847 cells from 4 melanoma 
patients. Data preprocessing, clustering, cell type annotation, differential 
expression, and pathway enrichment were conducted using Scanpy.

RESULTS
Non-responder samples exhibited a 2.3-fold increase in exhausted CD8+ T cells 
(42% vs 18%) and M2 macrophages (28% vs 12%)...

CONCLUSION
The results support the hypothesis that an immunosuppressive microenvironment 
driven by exhausted CD8+ T cells and M2 macrophages contributes to anti-PD-1 
resistance in melanoma.
```

#### Tính năng Export:
- **Export Markdown** → Đưa vào Overleaf/LaTeX
- **Export DOCX** → Gửi collaborator

#### Ý nghĩa:
- Tiết kiệm thời gian viết **first draft**
- Mỗi câu đều **link đến Evidence** → có thể verify
- Phù hợp chuẩn bị paper/grant proposal

---

## Q10: Tab Next Steps đề xuất gì? Priority phân loại như thế nào?

### Trả lời:

Tab Next Steps đề xuất các **hành động tiếp theo** để validation hoặc mở rộng nghiên cứu. AI không chỉ trả lời một lần mà còn **đồng hành xuyên suốt** dự án.

#### Các action trong prototype:

| Priority | Action | Tool |
|---|---|---|
| **HIGH** 🔴 | Run batch correction on bulk RNA-seq data | BBrowserX Pro |
| **HIGH** 🔴 | Validate exhaustion markers by flow cytometry | Experiment |
| **MEDIUM** 🟡 | Perform cell-cell communication analysis | CellChat via BioStudio |
| **MEDIUM** 🟡 | Run trajectory/pseudotime analysis on CD8+ T cells | BioStudio notebook |
| **MEDIUM** 🟡 | Build treatment response classifier | BioStudio ML notebook |
| **LOW** ⚪ | Search Talk2Data for cohorts with similar profiles | Talk2Data |

#### Phân loại Priority:
- **HIGH (Đỏ):** Cần làm **ngay** — thiếu bước này kết luận không đáng tin. Ví dụ: batch correction trước DEG.
- **MEDIUM (Vàng):** Nên làm — mở rộng phân tích. Ví dụ: trajectory analysis.
- **LOW (Trắng):** Có thể làm sau — tìm thêm reference. Ví dụ: search Talk2Data.

#### One-click routing:
Mỗi action có nút **"Run in [tool]"**. Click mở đúng công cụ với context hiện tại. Ví dụ:
- Click "Run in BBrowserX Pro" → Mở BBrowserX với dataset melanoma
- Click "Run in Talk2Data" → Search cohorts tương tự

#### Ý nghĩa:
- Xác định **điều gì cần làm tiếp** sau khi có kết quả
- Chuyển AI từ "chatbot" thành **"scientist copilot"**
- Đề xuất dựa trên **workflow chuẩn** của BioTuring ecosystem

---

## Bảng tóm tắt 8 tab

| Tab | Giống phần nào trong paper? | Câu hỏi nó trả lời | Người dùng nào cần |
|---|---|---|---|
| **Overview** | Abstract + Significance | "Tôi đang làm gì và đã đi đến đâu?" | PI, Collaborator |
| **Data** | Methods (Data acquisition) | "Dữ liệu có đủ tốt để phân tích không?" | Bioinformatician |
| **Literature** | Introduction/Background | "Kết luận này có căn cứ khoa học không?" | Reviewer, Student |
| **Analysis** | Methods + Results | "AI đã làm gì và tìm thấy gì?" | Data Scientist |
| **Evidence** | Supplementary Data | "Bằng chứng cho kết luận này ở đâu?" | Reviewer, PI |
| **Prediction** | Discussion/Future Directions | "Điều này có ý nghĩa sinh học gì?" | Biologist |
| **Report** | Full Manuscript Draft | "Tôi có thể viết paper từ đây không?" | First author |
| **Next Steps** | Future Work | "Tôi cần làm gì tiếp theo?" | Lab manager |

---

## Đường dẫn Source Code

Prototype được lưu tại:
```
/Users/admin/Documents/Coding/biostudio-ai-prototype/
```

File chính:
- `app/page.tsx` - Layout chính
- `app/components/ChatArea.tsx` - Chat + Charts
- `app/components/ResearchPanel.tsx` - Right Panel 8 tabs
- `app/components/JupyterNotebook.tsx` - Notebook Editor
- `app/data/mockData.ts` - Mock data
