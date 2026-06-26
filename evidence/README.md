# Bằng chứng (Evidence) — Day 22: LangSmith + Prompt Versioning

## Tổng quan

Thư mục này chứa đầy đủ 7 tệp bằng chứng cho 4 nhiệm vụ của lab.

## Danh sách bằng chứng

| Tệp | Mô tả |
|-----|-------|
| `01_langsmith_traces.png` | Ảnh chụp LangSmith dashboard với ≥ 50 traces |
| `02_prompt_hub.png` | Ảnh chụp Prompt Hub hiển thị 2 phiên bản prompt |
| `02_ab_routing_log.txt` | Log console của A/B routing (50 câu truy vấn, có nhãn v1/v2) |
| `03_ragas_scores.png` | Output terminal hiển thị bảng so sánh V1 vs V2 |
| `03_ragas_report.json` | Báo cáo JSON từ RAGAS evaluation |
| `04_pii_demo_log.txt` | Output console của PII detector (6 test cases) |
| `04_json_demo_log.txt` | Output console của JSON formatter (5 test cases) |

## Phân tích V1 vs V2

### Thiết kế Prompt

- **V1 (Ngắn gọn, thân thiện):** Hướng dẫn LLM trả lời trong 2-4 câu với ngôn ngữ đơn giản, dễ hiểu. Prompt này ưu tiên sự ngắn gọn và trực tiếp.

- **V2 (Chuyên nghiệp, có cấu trúc):** Yêu cầu LLM trả lời theo format có tổ chức (3-5 câu) với 3 phần: tóm tắt ý chính, giải thích chi tiết, và nêu mức độ chắc chắn. Prompt này ưu tiên depth và reasoning.

### Dự đoán kết quả

- **Faithfulness:** V1 có thể đạt điểm cao hơn vì câu trả lời ngắn gọn ít có khả năng chứa thông tin ngoài context. V2 với yêu cầu giải thích chi tiết có thể dẫn đến "hallucination" nhẹ.

- **Answer Relevancy:** V2 có thể đạt cao hơn vì yêu cầu trả lời có cấu trúc giúp bao phủ câu hỏi tốt hơn.

- **Context Recall/Precision:** Cả 2 version sử dụng cùng retriever nên context metrics sẽ tương đương. Sự khác biệt chủ yếu đến từ cách LLM sử dụng context.

### Kết luận

Việc so sánh 2 phong cách prompt cho thấy trade-off giữa ngắn gọn (V1) và chi tiết (V2). Trong production, việc chọn prompt version nên dựa trên use case cụ thể: V1 phù hợp cho chatbot FAQ nhanh, V2 phù hợp cho hệ thống phân tích chuyên sâu.
