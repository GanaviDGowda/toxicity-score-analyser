# Toxicity Monitoring System

An AI-powered comment moderation system that uses BERT to detect toxic comments, tracks user toxicity scores over time, and implements an automated warning and suspension system.

## Features

- **Real-time toxicity analysis** of user comments using BERT
- **Cumulative user scoring** with automatic decay over time
- **Progressive moderation** with warning and suspension thresholds
- **User history tracking** with time-based score decay
- **Simple web interface** for testing and monitoring

## Project Structure

```
toxicity-monitoring-system/
│
├── backend/
│   ├── app.py                # Flask API entry point
│   ├── model/                # Directory for the trained model
│   │   ├── toxicity_model.py # BERT model loading & prediction
│   ├── scheduler.py          # Score decay logic using APScheduler
│   ├── database.py           # MongoDB utilities
│   └── utils.py              # Scoring, thresholds, helper functions
│
├── data/                     # Dataset files
│   ├── jigsaw-toxic-comment-train.csv
│   ├── test.csv
│   ├── test_labels.csv
│   └── sample_submission.csv
│
├── train_model/              # Model training code
│   ├── train.py              # Train and export model
│   └── preprocessing.py      # Text cleaning/tokenization
│
├── frontend/                 # Simple web interface
│   ├── index.html
│   ├── style.css
│   └── app.js
│
├── requirements.txt          # Python dependencies
└── README.md                 # Project documentation
```

## Prerequisites

- Python 3.8+
- MongoDB
- Node.js and npm (for serving the frontend, optional)

## Installation

1. Clone this repository:
   ```
   git clone https://github.com/yourusername/toxicity-monitoring-system.git
   cd toxicity-monitoring-system
   ```

2. Install the Python dependencies:
   ```
   pip install -r requirements.txt
   ```

3. Make sure MongoDB is running on localhost:27017 (default)

## Usage

### Step 1: Train the Model

First, train the toxicity classification model using the Jigsaw dataset:

```bash
cd train_model
python train.py --data_path "../data/jigsaw-toxic-comment-train.csv" --num_epochs 2
```

This will train a BERT model and save it to the `backend/model/` directory.

### Step 2: Start the Backend Server

Start the Flask API server:

```bash
cd backend
python app.py
```

The server will run on http://localhost:5000 by default.

### Step 3: Serve the Frontend

You can serve the frontend using any static file server. For example, using Python's built-in HTTP server:

```bash
cd frontend
python -m http.server 8000
```

Then open http://localhost:8000 in your web browser.

### Step 4: Use the System

1. Enter a user ID in the "User ID" field
2. Type a comment in the text area
3. Click "Analyze" to check the toxicity score
4. View the user's score and status
5. Check the user's history by using the "Lookup" button

## System Design

### Toxicity Scoring

- Each comment is scored from 0-50 based on toxicity
- Higher toxicity scores have an exponentially higher impact on the user's cumulative score
- User scores decay by 5% daily
- Warning threshold: 80 points
- Suspension threshold: 200 points

### API Endpoints

- `POST /api/analyze` - Analyze a comment and update user score
- `GET /api/user/<user_id>` - Get user information and history

## Dataset

This project uses the Jigsaw Toxic Comment Classification dataset, which contains comments labeled for toxic behavior:

- toxic
- severe_toxic
- obscene
- threat
- insult
- identity_hate

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- [Jigsaw Toxic Comment Classification Challenge](https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge) for the dataset
- [Hugging Face Transformers](https://huggingface.co/transformers/) for the BERT implementation#   t o x i c i t y - s c o r e - a n a l y s e r 
 
 
