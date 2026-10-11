Структура репозитория


toxic-comments-moderation/
├── README.md
├── requirements.txt
├── .gitignore
├── configs/
│   ├── baseline.yaml
│   ├── rubert_token_cls.yaml
│   └── rubert_crf.yaml
│
├── data/
│   ├── raw/                     # исходный датасет Kaggle
│   ├── interim/                 # промежуточные данные
│   ├── processed/               # очищенные и подготовленные данные
│   └── annotated/               # ручная разметка типов и фрагментов
│
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   └── 02_annotation_analysis.ipynb
│
├── src/
│   ├── data/
│   │   ├── load_data.py
│   │   ├── preprocess.py
│   │   ├── convert_annotations.py
│   │   └── split_data.py
│   │
│   ├── annotation/
│   │   └── validate_spans.py
│   │
│   ├── models/
│   │   ├── baseline_tfidf.py
│   │   ├── rubert_token_cls.py
│   │   └── rubert_crf.py
│   │
│   ├── training/
│   │   ├── train_baseline.py
│   │   ├── train_token_cls.py
│   │   └── train_crf.py
│   │
│   ├── evaluation/
│   │   ├── classification_metrics.py
│   │   ├── span_metrics.py
│   │   └── robustness.py
│   │
│   └── inference.py
│
├── tests/
│   ├── test_preprocessing.py
│   ├── test_annotations.py
│   └── test_inference.py
│
├── experiments/
│   └── results.csv
│
└── reports/
    ├── figures/
    └── model_comparison.md
