# BioStudio AI - Research Panel Tabs Explanation

Date: 2026-05-08
Context: Giải thích chi tiết 8 tab trong Right Panel (Research State Panel) của BioStudio AI Prototype

---

## 1. Tab Overview (Tổng quan)

**Mục đích:** Tab quan trọng nhất, giống như **"tóm tắt luận án"** của cả quá trình nghiên cứu AI. Giúp nhà khoa học chỉ cần nhìn vào là hiểu ngay AI đang cố chứng minh điều gì, kết luận tạm thời là gì, và độ tin cậy ra sao.

### Các thành phần:

#### Objective (Mục tiêu nghiên cứu)
- **Ví dụ:** "Identify cell populations and molecular signatures associated with anti-PD-1 resistance in melanoma using single-cell transcriptomics."
- **Ý nghĩa:** Câu hỏi gốc mà nhà khoa học đặt ra. AI tự động trích xuất từ câu hỏi người dùng. Giúp kiểm tra xem **AI có hiểu đúng vấn đề** không (vd: nếu người dùng hỏi về spatial nhưng AI ghi bulk → cần sửa ngay).

#### Hypothesis (Giả thuyết)
- **Ví dụ:** "Exhausted CD8+ T cells and macrophage inflammatory signaling create an immunosuppressive microenvironment that drives anti-PD-1 resistance."
- **Ý nghĩa:** Giả thuyết AI đưa ra sau khi phân tích dữ liệu + tra Talk2Data. Không phải kết luận cuối cùng, mà là **"con đường AI đang đi"** để chứng minh. Nhà khoa học có thể đồng ý hoặc phản bác rồi điều chỉnh câu hỏi.

#### Current Conclusion (Kết luận hiện tại)
- **Ví dụ:** "Non-responder samples show significantly higher proportions of exhausted CD8+ T cells (42% vs 18%) and M2 macrophages (28% vs 12%)."
- **Ý nghĩa:** Kết quả thực tế sau khi AI chạy pipeline (QC → Clustering → Annotation → DEG). Hiển thị số liệu cụ thể để hỗ trợ kết luận.

#### Confidence (Độ tin cậy)
- **Giá trị:** 0.0 - 1.0 (ví dụ: **0.72** = 72%)
- **Phân loại:**
  - **< 0.6:** Thấp → Cần thêm dữ liệu hoặc thử lại
  - **0.6 - 0.8:** Trung bình → Kết luận có vẻ đúng nhưng cần validation
  - **> 0.8:** Cao → Có thể tin tưởng để viết paper
- **Caveat (Hạn chế):** Giải thích tại sao confidence không cao hơn (vd: "Limited to 4 patients. Cross-validation needed.")
- **Ý nghĩa:** Đây là điểm khác biệt quan trọng so với chatbot thông thường: AI **thừa nhận giới hạn** của nó.

#### Novelty Statement (Tính mới)
- **Ví dụ:** "This study links a specific exhausted CD8+ / M2 macrophage co-enrichment pattern to melanoma anti-PD-1 resistance with quantitative confidence scoring."
- **Ý nghĩa:** Giúp trả lời "Nghiên cứu này có gì mới?". AI so sánh với Talk2Data để xác định điểm độc đáo. Hữu ích khi viết abstract hoặc grant proposal.

---

## 2. Tab Data (Dữ liệu)

**Mục đích:** Hiển thị thông tin về tập dữ liệu đã upload, đánh giá chất lượng metadata, và danh sách file. Giúp nhà khoa học biết **AI đã hiểu đúng dữ liệu chưa** và **metadata có đủ chất lượng không**.

### Các thành phần:

#### Dataset
| Thuộc tính | Giá trị mẫu | Ý nghĩa |
|---|---|---|
| **Modality** | Single-cell RNA-seq (10x Genomics) | Loại kỹ thuật giải trình tự |
| **Cells** | 12,847 | Số lượng tế bào |
| **Genes** | 33,694 | Số lượng gene được đo |
| **Samples** | 4 patients | Số mẫu/bệnh nhân |
| **Groups** | 2 responders, 2 non-responders | Phân nhóm thí nghiệm |
| **Platform** | 10x Genomics Chromium v3 | Nền tảng công nghệ |

#### Metadata Quality
| Metadata | Quality | Ý nghĩa |
|---|---|---|
| Sample IDs | 100% | Đủ thông tin mẫu |
| Treatment status | 100% | Đủ nhãn điều trị |
| Response labels | 100% | Đủ nhãn phản ứng |
| Batch IDs | 50% | **Thiếu** → Cảnh báo batch effect |
| Clinical metadata | 75% | Gần đủ |
| Cell type labels | 0% | Chưa có → Cần annotation |

#### Uploaded Files
- `melanoma_scRNAseq.h5ad` (2.4 GB)
- `sample_metadata.xlsx` (45 KB)
- `patient_clinical_data.csv` (12 KB)

**Ý nghĩa trong workflow:** Xuất hiện ở **Bước 1** (Data understanding). AI tự động đọc file và báo cáo lại người dùng.

---

## 3. Tab Literature (Tài liệu tham khảo)

**Mục đích:** Hiển thị các nghiên cứu đã xuất bản liên quan. Giúp nhà khoa học **xác nhận kết luận AI có căn cứ khoa học** hay không, và ngăn AI bịa đặt (hallucination).

### Các thành phần:

| Paper | Tác giả | Năm | Tạp chí | Relevance |
|---|---|---|---|---|
| Single-cell profiling reveals immune suppression... | Jerby-Arnon et al. | 2018 | Cell | **95%** |
| T cell exhaustion in cancer... | Thommen & Schumacher | 2018 | Nature Reviews Cancer | **92%** |
| Macrophage-mediated immune suppression... | DeNardo & Ruffell | 2019 | Cancer Immunology Research | **88%** |
| Interferon signaling in tumor cells... | Benci et al. | 2019 | Nature Medicine | **84%** |
| Dissecting the tumor myeloid compartment... | Maier et al. | 2020 | Cancer Cell | **76%** |

### Ý nghĩa từng cột:
- **Relevance Score:** AI đánh giá mức độ liên quan đến kết quả hiện tại. 95% = cực kỳ liên quan.
- **DOI:** Liên kết đến bài báo gốc (nếu có).
- **Trong workflow:** Bước thứ 2 sau Data understanding. AI tự động search Talk2Data và PubMed.

---

## 4. Tab Analysis (Phân tích đã thực hiện)

**Mục đích:** Liệt kê chi tiết các phương pháp phân tích, tham số, và kết quả. Đây là phần **Methods** của nghiên cứu.

### Các analysis trong prototype:

#### 1. Cell type annotation
- **Method:** SingleR + marker-based manual curation
- **Parameters:** reference=HumanPrimaryCellAtlas, n_markers=98
- **Findings:** 12 cell types; CD8+ T cells 34.2%, Macrophages 18.7%, Melanoma 15.3%...

#### 2. Differential Expression: Responder vs Non-responder
- **Method:** Wilcoxon rank-sum (Scanpy)
- **Parameters:** min_pct=0.25, logfc_threshold=0.25, pval_cutoff=0.05
- **Findings:** 1,247 DEGs; PDCD1/HAVCR2/LAG3 upregulated; exhaustion signature enriched (NES=2.34, p<0.001)

#### 3. Pathway Enrichment
- **Method:** GSEA (fgsea) + GO BP
- **Parameters:** n_perm=10000, min_size=15, max_size=500
- **Findings:** T cell exhaustion, PD-L1, IFN-gamma enriched; cytotoxicity suppressed

### Ý nghĩa:
- **Transparency:** Kiểm tra tham số AI dùng (vd: resolution=0.8 có hợp lý không?)
- **Reproducibility:** Đủ thông tin để người khác replicate phân tích
- **Best-practice check:** So sánh với workflow chuẩn của BioTuring

---

## 5. Tab Evidence (Bằng chứng)

**Mục đích:** Liên kết tất cả các entities (tế bào, gene, pathway, cohort) và outputs (biểu đồ, bảng) để tạo thành **chuỗi bằng chứng** hỗ trợ kết luận. Mỗi kết luận AI đưa ra đều có thể **truy ngược** về bằng chứng gốc.

### Các nhóm evidence:

#### Cells / Clusters
| Entity | Mô tả | Nguồn | Confidence |
|---|---|---|---|
| CD8+ T cells (Cluster 7) | Exhausted, PDCD1+/HAVCR2+/LAG3+ | SingleR annotation | **89%** |
| Macrophages (Cluster 4) | M2-like, CCL2+/CCL3+/MRC1+ | Marker-based | **84%** |
| Melanoma (Cluster 2) | IFN response, IFIT1+/IFIT3+ | Tumor scoring | **78%** |

#### Genes / Markers
| Gene | Mô tả | Giá trị |
|---|---|---|
| PDCD1 (PD-1) | Exhaustion marker, log2FC=3.42 | Up in NR |
| HAVCR2 (TIM-3) | Exhaustion marker, log2FC=2.89 | Up in NR |
| LAG3 | Exhaustion marker, log2FC=2.76 | Up in NR |

#### Pathways
- T cell exhaustion: GSEA NES=2.34, FDR=0.0012
- PD-L1 expression: GSEA NES=2.13, FDR=0.0034
- IFN-gamma response: GSEA NES=1.99, FDR=0.0056

#### Cohorts / Datasets
- GSE123813: Jaccard similarity=0.62
- GSE145286: Jaccard similarity=0.67

#### Notebook Outputs
- UMAP plot (cell 6): 12 clusters
- Composition bar chart (cell 8): 7 cell types
- DEG table (cell 9): 1,247 genes

### Ý nghĩa:
- **Audit trail:** Reviewer có thể kiểm tra từng bước
- **Connected ecosystem:** Liên kết cell → gene → pathway → cohort → notebook output

---

## 6. Tab Prediction (Dự đoán)

**Mục đích:** AI không chỉ phân tích "đã xảy ra gì", mà còn **dự đoán ý nghĩa sinh học** bằng cách so sánh với curated references. Đây là **điểm mạnh độc đáo** của BioStudio AI so với chatbot thông thường.

### Các dự đoán trong prototype:

#### 1. Cell State Prediction
- **Prediction:** High exhausted CD8 T-cell signature in non-responders
- **Confidence:** 89%
- **Evidence:** PDCD1, HAVCR2, LAG3 upregulated; Exhaustion score: 0.84 vs 0.31
- **Caveats:** Limited to 4 patients; Single timepoint

#### 2. Phenotype Prediction
- **Prediction:** Immune-resistant phenotype (cold tumor conversion)
- **Confidence:** 72%
- **Evidence:** M2 macrophages 28% vs 12%; Decreased cytotoxic function
- **Caveats:** Needs cross-validation; Spatial data would strengthen prediction

#### 3. Similar Cohort
- **Prediction:** Closest match: Anti-PD-1 melanoma non-responders (GSE145286)
- **Confidence:** 78%
- **Evidence:** Jaccard similarity of DEGs: 0.67; Shared cell composition
- **Caveats:** Different sequencing platform (SMART-seq2 vs 10x)

### Cấu trúc mỗi prediction bao gồm:
- **Input features:** Dữ liệu gốc đưa vào
- **Reference datasets:** Talk2Data/public datasets so sánh
- **Comparable cell populations:** Cell types tương đồng
- **Confidence score:** Độ tin cậy (0-1)
- **Limitations (Caveats):** Giới hạn của dự đoán
- **Recommended validation:** Cách xác minh tiếp theo

### Ý nghĩa:
- Giúp nhà khoa học **tạo hypothesis mới** thay vì chỉ mô tả dữ liệu
- Confidence + caveats giúp tránh **over-interpretation**

---

## 7. Tab Report (Báo cáo)

**Mục đích:** Tự động tạo bản thảo manuscript-ready từ toàn bộ nghiên cứu (MVP 5: Publication Copilot).

### Nội dung mẫu:

```
AI-Generated Research Report: Melanoma Treatment Resistance

OBJECTIVE
Identify cell populations and molecular signatures associated with anti-PD-1 
resistance in melanoma using single-cell transcriptomics.

METHODS
Single-cell RNA-seq analysis was performed on 12,847 cells from 4 melanoma 
patients (2 responders, 2 non-responders). Data preprocessing, clustering, 
cell type annotation, differential expression, and pathway enrichment were 
conducted using Scanpy and custom BioTuring workflows.

RESULTS
Non-responder samples exhibited a 2.3-fold increase in exhausted CD8+ T cells 
(42% vs 18%) and M2 macrophages (28% vs 12%). Differential expression analysis 
identified 1,247 DEGs in CD8+ T cells, with key exhaustion markers PDCD1, 
HAVCR2, and LAG3 significantly upregulated. Pathway analysis confirmed 
enrichment of T cell exhaustion and PD-L1 expression pathways in non-responders.

CONCLUSION
The results support the hypothesis that an immunosuppressive microenvironment 
driven by exhausted CD8+ T cells and M2 macrophages contributes to anti-PD-1 
resistance in melanoma.
```

### Tính năng:
- **Export Markdown:** Xuất `.md` để đưa vào Overleaf/LaTeX
- **Export DOCX:** Xuất Word để gửi collaborator
- **Linked statements:** Mỗi câu trong report liên kết trực tiếp đến analysis output

### Ý nghĩa:
- Tiết kiệm thời gian viết **first draft**
- Mỗi câu đều **có thể verify** được từ tab Evidence

---

## 8. Tab Next Steps (Các bước tiếp theo)

**Mục đích:** AI đề xuất các thí nghiệm/phân tích tiếp theo để **validation** hoặc **mở rộng** nghiên cứu. Biến AI từ "trả lời một lần" thành **đồng hành xuyên suốt** dự án.

### Các action trong prototype:

| Priority | Action | Tool | Category |
|---|---|---|---|
| **HIGH** 🔴 | Run batch correction on bulk RNA-seq data | BBrowserX Pro | Analysis |
| **HIGH** 🔴 | Validate exhaustion markers by flow cytometry | Experiment | Validation |
| **MEDIUM** 🟡 | Perform cell-cell communication analysis | CellChat via BioStudio | Analysis |
| **MEDIUM** 🟡 | Run trajectory/pseudotime analysis on CD8+ T cells | BioStudio notebook | Analysis |
| **MEDIUM** 🟡 | Build treatment response classifier | BioStudio ML notebook | Prediction |
| **LOW** ⚪ | Search Talk2Data for cohorts with similar profiles | Talk2Data | Literature |

### Ý nghĩa:
- **Priority ranking:** Biết nên làm gì **trước** (high) và gì để sau (low)
- **One-click run:** Mỗi action có nút "Run in [tool]" — ví dụ click mở BBrowserX Pro với context hiện tại
- **Workflow continuity:** AI đồng hành từ câu hỏi ban đầu → phân tích → validation → xuất bản

---

## Bảng so sánh tóm tắt 8 tab

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

## Research Panel trong Product UX

Theo tài liệu gốc, BioStudio AI sử dụng **three-panel workspace**:

```
┌─────────────┬──────────────────────────────┬────────────────┐
│   LEFT      │           CENTER             │     RIGHT      │
│             │                              │                │
│  Research   │    Chat + Results + Charts   │  Research      │
│  Threads    │                              │  State Panel   │
│  Projects   │  (UMAP, DEG table, etc.)     │  (8 tabs)      │
│  Data       │                              │                │
│             │                              │                │
└─────────────┴──────────────────────────────┴────────────────┘
```

Right Panel chuyển chat từ **"câu trả lời một lần"** thành **"workflow nghiên cứu có thể truy vết"** — nhà khoa học không chỉ cần câu trả lời, mà cần biết **tại sao câu trả lời đáng tin**, **dữ liệu nào hỗ trợ**, và **làm gì tiếp theo**.
