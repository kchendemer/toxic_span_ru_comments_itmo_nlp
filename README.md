# Explainable Moderation of Russian-Language Comments

## Структура репозитория

```text
toxic-comments-moderation/
├── README.md
├── requirements.txt
├── .gitignore
│
├── configs/
│   ├── baseline.yaml
│   ├── rubert_token_cls.yaml
│   └── rubert_crf.yaml
│
├── data/
│   ├── raw/                      # Исходный датасет Kaggle
│   ├── interim/                  # Промежуточные данные
│   ├── processed/                # Подготовленные данные
│   └── annotated/                # Данные с ручной разметкой
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
```

## Описание проекта

Проект посвящён выявлению токсичности в русскоязычных комментариях, классификации типов токсичности и выделению соответствующих фрагментов текста.

### Типы токсичности

1. `Normal` — нормальный, нетоксичный комментарий.
2. `Threat` — угроза.
3. `Insult` — оскорбление.
4. `Identity_attack` — нападение на социальную группу.
5. `Profanity` — ненормативная лексика.

Если комментарий содержит несколько типов токсичности, каждый тип представлен отдельной строкой с общим идентификатором исходного комментария. Для нетоксичных комментариев фрагмент токсичности не размечается.

### Используемые подходы

1. **TF-IDF + Logistic Regression** — базовая модель классификации.
2. **RuBERT + Token Classification** — классификация токенов для выделения токсичных фрагментов.
3. **RuBERT + CRF** — выделение токсичных фрагментов с учётом последовательности меток.

### Датасет

Russian Language Toxic Comments — [Kaggle](https://www.kaggle.com/datasets/blackmoon/russian-language-toxic-comments).

Исходные данные хранятся в `data/raw/`, подготовленные — в `data/processed/`, данные с дополнительной ручной разметкой — в `data/annotated/`.

### Оценка качества

* **Macro-F1** — классификация типов токсичности.
* **F1 токсичного класса** — бинарное определение токсичности.
* **Character-level F1** — качество выделения токсичных фрагментов.
* **Robustness evaluation** — устойчивость к маскировке токсичных слов.

### Запуск проекта

Установка зависимостей:

```bash
pip install -r requirements.txt
```

Подготовка данных:

```bash
python -m src.data.preprocess
```

Обучение моделей:

```bash
python -m src.training.train_baseline
python -m src.training.train_token_cls
python -m src.training.train_crf
```

Результаты экспериментов сохраняются в `experiments/results.csv`, а итоговое сравнение моделей — в `reports/model_comparison.md`.