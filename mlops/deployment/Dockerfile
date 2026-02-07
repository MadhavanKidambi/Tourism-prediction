
FROM python:3.10-slim

# Create non-root user
RUN useradd -m -u 1000 user

ENV HOME=/home/user \
    PATH=/home/user/.local/bin:$PATH

WORKDIR $HOME/app

# Copy only requirements first 
COPY requirements.txt .

RUN pip install --no-cache-dir numpy==1.26.4

# Install deps as root
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the app
COPY --chown=user . .

# Switch to non-root user
USER user

EXPOSE 8501

CMD ["streamlit", "run", "app.py", "--server.port=7860", "--server.address=0.0.0.0", "--server.enableXsrfProtection=false"]
