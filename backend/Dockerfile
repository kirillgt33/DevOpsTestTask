FROM python:3.11-slim

WORKDIR /app

RUN useradd -m myuser
USER myuser

COPY --chown=myuser:myuser app.py .

EXPOSE 8080

CMD ["python", "app.py"]