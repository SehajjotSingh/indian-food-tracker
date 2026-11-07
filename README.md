# Indian Food Tracker

A Streamlit prototype for estimating nutrition from Indian meals. Enter food names and quantities manually or upload a food photo for an image-classifier prediction, then review estimated calories, protein, fat, and carbohydrates in a session-based food log. The app also calculates BMI and estimated daily calorie needs from the profile values you enter.

> **Prototype, not medical advice.** Food recognition and nutrition matching are approximate. Results can be wrong, especially for mixed dishes, portion sizes, recipes, and foods not represented in the dataset. Do not use these estimates for medical or clinical decisions.

## Features

- **Manual food entry:** Enter foods such as `2 Chapati and 1 Dal`; fuzzy matching finds likely entries in the nutrition dataset.
- **Photo-based suggestions:** Upload a JPG, JPEG, or PNG image. A Hugging Face image-classification model suggests foods, and matching results can be added to the log.
- **Nutrition summary:** Review estimated calories, protein, fat, and carbohydrates for items added during the current Streamlit session.
- **Profile estimates:** Calculate BMI and an estimated daily calorie target using weight, height, age, gender, and activity level.
- **Food log controls:** View logged items and clear the current session's log.

## Getting started

### Requirements

- Python installed in a virtual environment
- Internet access for the first run, so the Hugging Face model can be downloaded
- Enough disk space and memory for PyTorch and the image-classification model

### Install and run

From the repository root:

```bash
python -m venv .venv
```

Activate the environment:

```bash
# macOS / Linux
source .venv/bin/activate

# Windows PowerShell
.venv\Scripts\Activate.ps1
```

Install dependencies and launch the app:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
streamlit run app.py
```

Streamlit will print a local URL (usually `http://localhost:8501`) to open in your browser. The first launch may take longer while the model `NOTGOD6000/finetuned-indian-food` is downloaded and loaded.

## How to use

1. Set your profile in the sidebar to see BMI and an estimated daily calorie target.
2. In **Manual Entry**, type food names and quantities, then add matched foods to your log.
3. In **Upload Image**, choose a food photo, review the model's suggestions, and add suitable matches.
4. Review the nutrition totals and food log below the tabs. Use **Clear Log** to reset it.

The food log is stored in Streamlit session state; it is not a permanent diary and may not persist after the session ends or the app restarts.

## Data and model

- The main app (`app.py`) reads `indian_food_with_nutrition_v4.csv`.
- The repository also includes `indian_food_with_nutrition_v3.csv`, used by the earlier phase examples.
- Image suggestions use the Hugging Face model [`NOTGOD6000/finetuned-indian-food`](https://huggingface.co/NOTGOD6000/finetuned-indian-food).
- Nutrition matching uses RapidFuzz's `WRatio` scorer and a matching threshold in the app. A fuzzy match is only a best-effort name match, not verification that the pictured food or portion is correct.
- Check the CSV's units and serving basis before interpreting its nutrition values; totals scale the dataset values by the quantity entered.

## Repository contents

```text
.
├── app.py                                 # Main Streamlit app
├── phase1_app.py                          # Early prototype with sample nutrition values
├── phase2_app.py                          # Earlier manual-entry prototype using CSV data
├── phase3_app.py                          # Earlier image-classification prototype
├── indian_food_image_classification.ipynb # Image-classification notebook
├── indian_food_with_nutrition_v3.csv      # Earlier nutrition dataset
├── indian_food_with_nutrition_v4.csv      # Dataset used by the main app
├── requirements.txt                       # Python dependencies
└── README.md
```

## Notes and limitations

- Image classification can confuse visually similar foods and may not recognize mixed dishes, ingredients, or regional variations.
- The app estimates nutrition from dataset entries; it does not measure serving size from an image.
- BMI and daily calorie needs are rough estimates, not diagnoses or personalized medical guidance.
- The food log is session-based and does not currently provide durable storage or account-based syncing.

## License

No license file is currently included. Unless a license is added, do not assume that the code or bundled data can be reused or redistributed.
