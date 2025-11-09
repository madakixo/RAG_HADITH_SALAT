Hadith Wisdom: Advanced RAG System with Prayer ReflectionsOverviewHadith Wisdom is an advanced Retrieval-Augmented Generation (RAG) system built with Streamlit for querying authentic Hadith collections. It integrates:Hybrid Retrieval: Combines BM25 (keyword-based) and FAISS (dense embeddings with cosine similarity) for initial candidate selection.
Cross-Encoder Reranking: Uses a fine-tuned cross-encoder (ms-marco-MiniLM-L-6-v2) to rerank candidates for higher relevance.
Generative Summarization: T5-small model generates ethical/spiritual takeaways from retrieved Hadiths.
Prayer Times Integration: Astronomical calculations for accurate prayer times in selected locations, with post-prayer Hadith reflections.
Bilingual Support: English and Arabic Hadith texts/grades/comments.

The system supports simulated data out-of-the-box (expandable via CSV uploads). It's designed for educational, spiritual, and research use.Key Features:Chat-like Hadith search with relevance scores.
Top-K results display with expanders.
Prayer times dashboard with recent prayer reflections.
Downloadable JSON exports.
Cached setup for fast reloads.

Demo
Run the app locally to query Hadiths (e.g., "patience in trials") or view prayer times for Lagos/Abuja/Cairo/Makkah.Screenshot (Placeholder: Add actual screenshot in repo)ArchitectureData Loading: Loads bilingual Hadith CSVs or simulates data; caches as JSON.
Embedding & Indexing: SentenceTransformer for dense vectors; FAISS for cosine search; BM25 for sparse.
Retrieval Pipeline:Hybrid: Retrieve 20 candidates.
Rerank: Cross-encoder scores query-doc pairs; select top-5.


Generation: T5 summarizes with context.
UI: Streamlit tabs for search/reflections; sidebar for settings.

RequirementsPython VersionPython 3.9+ (tested on 3.12)

DependenciesCreate a requirements.txt file and install via pip install -r requirements.txt.

streamlit==1.38.0
pandas==2.2.2
numpy==1.26.4
torch==2.4.1
faiss-cpu==1.8.0  # Use faiss-gpu for CUDA
sentence-transformers==3.0.1
transformers==4.45.1
rank-bm25==0.2.2
pickle5==0.0.11  # For older Python; optional in 3.9+

Notes:faiss-cpu for CPU; switch to faiss-gpu if CUDA available.
No additional installs needed for core libs (e.g., datetime, math are stdlib).
For production: Pin versions to avoid breaks.

Install:bash

pip install -r requirements.txt

Setup & InstallationClone/Setup Repo:bash

git clone <your-repo-url>
cd hadith-rag-app

Install Dependencies:bash

pip install -r requirements.txt

Data Preparation (Optional):Altammami, S , Atwell, E and Alsalka. 'The Arabic–English Parallel Corpus of Authentic Hadith'. 
In: International Journal on Islamic Applications in Computer Science And Technology - IJASAT. International Conference on 
Islamic Applications in Computer Science and Technologies - IMAN 2019, 27-28 Dec 2019.
http://www.sign-ific-ance.co.uk/index.php/IJASAT/article/view/2199/1908

Run the App:bash

streamlit run app.py  # Replace 'app.py' with your main file

Opens at http://localhost:8501.
First run: Builds/caches embeddings (~1-2 min; subsequent runs faster).

Customization:Add locations: Edit PRAYER_LOCATIONS dict.
Expand queries: Update PRAYER_QUERIES or QUERY_EXAMPLES.
Bilingual: Toggle via sidebar; Arabic needs UTF-8 support.

Troubleshooting:CUDA Errors: Install faiss-gpu and ensure torch CUDA version matches.
Model Downloads: HuggingFace cache (~500MB); ensure internet on first run.
Data Issues: Check console for logs; simulated data falls back automatically.

How to Use RAG QueryThe RAG query is the core search feature in the  Advanced Hadith Search tab. It leverages the full pipeline for precise, context-aware results.Step-by-Step UsageLaunch App:Run streamlit run app.py.
Navigate to  Advanced Hadith Search tab.

Configure Settings (Sidebar):Language: English (default) or Arabic for reflections/texts.
Quick Searches: Click examples like "Rewards for good character" to auto-fill.

Enter Query:In the chat input: Type a natural language query, e.g.:"Hadith on patience during trials"
"Importance of Fajr prayer rewards"
"Prophet's sayings on family kindness"

Press Enter or click send.

View Results:Assistant Response: Generated summary/takeaway (e.g., "Patience is a pillar of faith...").
Expanded Hadiths: Click expanders for top-5 reranked results:Shows relevance score (0-1; higher = better match).
Displays chapter, grade, full text, Isnad, Matn.
Arabic toggle if selected.

Chat History: Scrolls with previous queries/responses.

Export:Click  Download Results to get JSON with query, response, and Hadiths.

Example WorkflowQuery: "Rewards for good character"
Retrieval: Hybrid fetches 20 candidates; cross-encoder reranks to top-5.
Output:

Assistant: Good character elevates one's status in Islam, akin to prayer and fasting...

📜 Hadith #1 (Relevance: 0.85)
**Chapter:** Book of Manners | **Grade:** Sahih
**Text:** The Prophet said, "The heaviest thing on the scales will be good character..."

Advanced TipsQuery Tips: Use specific keywords for better BM25; semantic phrases for embeddings. E.g., "exact phrase" for quotes.
Reranking Insight: Scores >0.7 indicate strong matches; app logs full pipeline in console.
Prayer Integration: In  Prayer Reflections, recent prayers auto-trigger RAG queries (e.g., post-Asr Hadith).
Extending: Modify advanced_retrieve() for custom weights (e.g., 0.7 BM25 + 0.3 cosine).
Performance: Cached; ~2-5s/query. Scale with more data via CSVs.

ContributingIssues: Report bugs in GitHub Issues.
Enhancements: Add CSVs, new rerankers (e.g., Cohere), or UI themes.
License: MIT (add to repo).

LicenseMIT License. See LICENSE for details.Built with  for spiritual growth. Questions? Open an issue! 

