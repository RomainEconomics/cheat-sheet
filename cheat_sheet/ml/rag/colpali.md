# ColPali

- [Paper](https://arxiv.org/pdf/2407.01449)
- [HF Blog](https://huggingface.co/blog/manu/colpali)
- [Cookbook](https://github.com/tonywu71/colpali-cookbooks)
- [Cookbook v2](https://github.com/weaviate/recipes/blob/main/weaviate-features/named-vectors/NamedVectors-ColPali-POC.ipynb)

ColPali is a retrieval model, with a Lora adapter on top of PaliGemma.
ColPali is interpretable due to its MaxSim scoring where you can highlight the areas of the image of the PDF.

Using ColPali removes the need for potentially complex and brittle layout recognition and OCR pipelines with a single model that can take into account both the textual and visual content (layout, charts, ...) of a document.

```python
from byaldi import RAGMultiModalModel

file_path = "ENG_URD2023_FR_VMEL_24-03-08.pdf"

# 1. Index Documents
RAG = RAGMultiModalModel.from_pretrained("vidore/colpali")

RAG.index(
   input_path=file_path,
index_name="pdf_index",  # index will be saved at index_root/index_name/
store_collection_with_index=False,
overwrite=True,
)

text_query = "What are the CAPEX aligned and eligible of the company when regarding the EU taxonomy Total A1+A2 (non aligned to taxonomy)"
results = RAG.search(text_query, k=5)


# 2. Or reuse indexing directly
RAG = RAGMultiModalModel.from_index("pdf_index")

text_query = "What are the CAPEX aligned and eligible of the company when regarding the EU taxonomy Total A1+A2 (non aligned to taxonomy)"
results = RAG.search(text_query, k=5)
print(results)
```
