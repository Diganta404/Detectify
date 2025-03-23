# Detectifiy - Deepfake Detection Web Application

A Flask-based web application for detecting deepfake videos and AI-generated audio using machine learning models.

## Features

- Video deepfake detection
- Audio AI-generation detection
- User-friendly web interface with modern dark mode design
- Real-time processing
- Detailed analysis results with confidence scores
- Responsive design for desktop and mobile devices

## Setup Instructions

1. Create a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Download sample data (optional but recommended for training):
```bash
# Download all sample data (recommended)
python -m app.utils.download_all_samples

# Or download specific datasets
python -m app.utils.download_samples  # Basic samples
python -m app.utils.download_deepfake_samples  # Deepfake video samples
python -m app.utils.download_audio_samples  # AI-generated audio samples
```

4. Train the models (optional but recommended):
```bash
python -m app.utils.train_models
```

5. Run the application:
```bash
python app.py
# Or use the run script with better error handling
python run.py
```

6. Access the application at `http://localhost:5000`

## Project Structure

```
Detectifiy/
├── app/
│   ├── datasets/           # Sample datasets for training
│   │   ├── audio/
│   │   │   ├── fake/       # AI-generated audio samples
│   │   │   └── real/       # Real audio samples
│   │   └── video/
│   │       ├── fake/       # Deepfake video samples
│   │       └── real/       # Real video samples
│   ├── models/             # ML model definitions
│   │   ├── detector.py     # Main detector implementation
│   │   └── trained/        # Trained model weights
│   ├── static/             # Static assets
│   │   ├── css/            # Stylesheets
│   │   ├── js/             # JavaScript files
│   │   └── uploads/        # Uploaded media files
│   ├── templates/          # HTML templates
│   │   ├── base.html       # Base template
│   │   └── index.html      # Main page template
│   └── utils/              # Utility scripts
│       ├── download_samples.py        # Script to download basic sample data
│       ├── download_deepfake_samples.py  # Script to download deepfake samples
│       ├── download_audio_samples.py  # Script to download audio samples
│       ├── download_all_samples.py    # Script to download all sample data
│       └── train_models.py            # Script to train the models
├── app.py                  # Main Flask application
├── run.py                  # Run script with better error handling
├── requirements.txt        # Python dependencies
└── README.md               # This file
```

## Model Information

### Video Deepfake Detection
- **Architecture**: ResNet50-based neural network with custom classification layers
- **Input**: Video frames resized to 224x224 pixels
- **Process**: Each frame is analyzed individually, then results are aggregated
- **Output**: Binary classification (REAL/FAKE) with confidence score

### Audio AI Detection
- **Architecture**: Custom CNN model for spectrogram analysis
- **Input**: Mel spectrograms generated from audio files
- **Process**: Analyzes frequency patterns characteristic of AI-generated audio
- **Output**: Binary classification (REAL/AI GENERATED) with confidence score

## Dataset Information

The application requires sample data for training the models. You can download sample data using the provided scripts:

```bash
# Download all sample data
python -m app.utils.download_all_samples
```

This will download:
- Real videos from public sources
- Sample deepfake videos (if available)
- Real audio samples from FreeSound
- Sample AI-generated audio (if available)

For more comprehensive datasets, consider downloading from these sources:

### Video Datasets:
1. **FaceForensics++**: https://github.com/ondyari/FaceForensics
2. **Deepfake Detection Challenge**: https://ai.facebook.com/datasets/dfdc/
3. **Celeb-DF**: https://github.com/yuezunli/celeb-deepfakeforensics

### Audio Datasets:
1. **ASVspoof**: https://www.asvspoof.org/
2. **WaveFake**: https://github.com/RUB-SysSec/WaveFake
3. **FakeAVCeleb**: https://github.com/DASH-Lab/FakeAVCeleb

## Training the Models

To train the models on your dataset:

1. Ensure you have sample data in the dataset directories
2. Run the training script:
```bash
python -m app.utils.train_models
```
3. The trained models will be saved in `app/models/trained/`

## How Detection Works

1. **Video Deepfake Detection**:
   - Frames are extracted from the uploaded video
   - Each frame is processed through the ResNet50-based model
   - The model analyzes visual artifacts and inconsistencies
   - Results are aggregated to determine if the video is authentic or manipulated

2. **Audio AI Detection**:
   - The audio is converted to a mel spectrogram representation
   - The spectrogram is analyzed by the CNN model
   - The model identifies patterns typical of AI-generated audio
   - A final prediction is made based on the detected patterns

## Security Note

This application is for demonstration purposes. For production use, implement additional security measures and API rate limiting.

## Troubleshooting

- **Model Loading Issues**: Ensure TensorFlow is properly installed for your platform
- **File Upload Errors**: Check that the upload directory exists and has proper permissions
- **Processing Errors**: Verify that the uploaded files meet the format and size requirements
- **Dataset Download Issues**: If automatic download fails, manually download from the provided links

