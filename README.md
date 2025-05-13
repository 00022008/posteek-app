# Posteek

A modern social media platform built with FastAPI and React.

## Project Structure

```
posteek/
├── backend/         # FastAPI backend
├── frontend/        # React frontend
└── workers/         # Background workers
```

## Setup and Installation

### Backend

1. Create and activate virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

2. Install dependencies:
```bash
cd backend
pip install -r requirements.txt
```

3. Set up environment variables:
```bash
cp .env.example .env
# Edit .env with your configuration
```

4. Run the development server:
```bash
uvicorn main:app --reload
```

### Frontend

1. Install dependencies:
```bash
cd frontend
npm install
```

2. Run development server:
```bash
npm run dev
```

## Deployment

### Backend Deployment (GCP)

1. SSH into your GCP VM:
```bash
gcloud compute ssh [INSTANCE_NAME]
```

2. Clone the repository:
```bash
git clone [YOUR_REPO_URL]
cd posteek
```

3. Set up the environment:
```bash
python -m venv venv
source venv/bin/activate
pip install -r backend/requirements.txt
```

4. Configure environment variables:
```bash
cp backend/.env.example backend/.env
# Edit .env with production settings
```

5. Set up systemd service:
```bash
sudo nano /etc/systemd/system/posteek.service
```

Add the following configuration:
```ini
[Unit]
Description=Posteek Backend
After=network.target

[Service]
User=your_user
WorkingDirectory=/path/to/posteek/backend
Environment="PATH=/path/to/posteek/venv/bin"
ExecStart=/path/to/posteek/venv/bin/uvicorn main:app --host 0.0.0.0 --port 8000

[Install]
WantedBy=multi-user.target
```

6. Start the service:
```bash
sudo systemctl start posteek
sudo systemctl enable posteek
```

### Domain Configuration

1. Point your domain (posteek.com) to your GCP VM's IP address
2. Set up SSL certificates using Let's Encrypt
3. Configure Nginx as a reverse proxy

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

This project is licensed under the MIT License. 