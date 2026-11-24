# Breccia Rock Classification App

A Streamlit and TensorFlow application for classifying breccia rock images into geology logging categories.

## Features

- Upload multiple breccia rock images.
- Preview uploaded images in the app.
- Resize images to the model's expected dimensions.
- Run an image classification TensorFlow model.
- Export predictions to an Excel workbook.
- Use drillhole and interval information encoded in image filenames.

## Supported classifications

The classifier maps model predictions to these classes:

- `1BX`
- `2BX`
- `3BX`
- `CAVBX`
- `FBX`
- `MBX`
- `NBX`

## Project structure

```text
NGM-APP/
├── breccia_rock_.py
├── Breccia_Rock_classsifier.ipynb
├── Breccia_Rock_Classifier.h5
├── requirements.txt
├── LICENSE
└── Extras/
    ├── nevadaimage.jfif
    └── ngm.jfif
```

## Requirements

The project uses:

- Python
- Streamlit
- TensorFlow/Keras
- NumPy
- pandas
- Pillow
- natsort
- XlsxWriter
- Altair
- scikit-learn
- Jupyter/nbformat

Install the dependencies:

```bash
pip install -r requirements.txt
```

## Run the application

From the repository directory:

```bash
streamlit run breccia_rock_.py
```

Open the URL printed by Streamlit, usually:

```text
http://localhost:8501
```

## Usage

1. Upload one or more breccia images.
2. Confirm that filenames include the hole ID and depth interval.
3. Select **Predict** to run the classifier.
4. Review the predicted geology labels.
5. Download the results as an Excel file.

## Expected image filenames

The app extracts drillhole information from image filenames using underscore-separated fields.

Example:

```text
HOLEID_FROM_TO.jpg
```

The first field is used as the hole ID, followed by the geological `GeoFrom` and `GeoTo` interval values.

Example:

```text
MOR25-5534_1200_1210.jpg
```

## Model behavior

The application:

1. Saves uploaded images to a temporary `Breccia_Rock` directory.
2. Resizes images to `400 x 600` pixels.
3. Applies image rescaling with `1 / 255`.
4. Runs `Breccia_Rock_Classifier.h5`.
5. Converts model probabilities to the predicted breccia class.
6. Builds a pandas DataFrame containing:

```text
HoleID
GeoFrom
GeoTo
Predicted_Labels
```

7. Exports the prediction table to Excel.

## Model file

The trained model is stored as:

```text
Breccia_Rock_Classifier.h5
```

The app downloads the model automatically if `model.h5` is not present locally.

## Notebook

`Breccia_Rock_classsifier.ipynb` contains the model development and training workflow.

Use the notebook to:

- Explore breccia image data.
- Prepare image datasets.
- Train or refine the classifier.
- Export an updated model file.

## License

MIT License. See [LICENSE](LICENSE).
