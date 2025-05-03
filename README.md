

# Secure Note-Keeping Web App

This web application securely allows users to create and store notes using both symmetric and asymmetric encryption algorithms.

---

## Introduction

The project uses:

* Frontend: HTML, CSS, JavaScript
* Backend: Django (Python)
* Web Server: Nginx
* Deployment: Docker using an Alpine Linux base image

The goal is to ensure secure storage and transmission of user notes.

---

## Installation Guide

### 1. Requirements

Before installing, ensure the following:

* Your system is running Linux (preferably Debian 12 or Bookworm).
* Docker is installed using the official Docker installation guide. Do not use `docker.io` or other unofficial sources.
* At least 500 MB of free disk space is available.
* Docker video installation guides:

  * Chris’s YouTube Docker setup: [https://www.youtube.com/watch?v=94VQvRpjfO8\&t=726s](https://www.youtube.com/watch?v=94VQvRpjfO8&t=726s)
  * Official Docker Docs: [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/)
* Optional: Installation video for this project – [https://youtu.be/Rv8N2DZc\_Mo](https://youtu.be/Rv8N2DZc_Mo)

---

### 2. Installation Steps

1. **Verify the Archive**


2. **Pre-Pull Docker Images (Optional)**

   * Pull Docker images from Docker Hub in advance to save setup time.

3. **Extract and Navigate**

   * Extract the secure archive:

     * `tar -xvf securenote.tar.xz`
   * Change directory:

     * `cd securenote`

4. **Build and Run the Application**

   * Use the following command to build and run:

     * `docker compose up --build`

5. **Handle Database Timing Issues**

   * If errors appear (e.g., Django migrations fail), wait a few seconds until the PostgreSQL database is ready.
   * Then re-run the app using:

     * `docker compose up`
   * This issue is generally handled automatically via a sleep delay added in the main process.

6. **Build the Image Separately (Optional)**

   * If preferred, you can build the image separately:

     * `docker compose build`
   * Then run it:

     * `docker compose up`

7. **Set Up Custom Domain (Optional)**


8. **Access the App**

   * Open your browser and visit any of the following:

     * [https://localhost](https://localhost)
     * [https://127.0.0.1](https://127.0.0.1)
     
   * The app will automatically redirect HTTP traffic to HTTPS.
   * Only traffic from the above domains will be accepted due to Django's security settings.

---

## Features

**User Authentication**

* Secure login, logout, registration
* Password update, reset, and forget features

**Note Management**

* Users can create, update, and delete their notes

**Data Encryption**

* Notes are encrypted using a user-specific AES key
* Encrypted data is stored as binary in the database

**Key Management**

* The user's AES key is encrypted using their public key
* The server signs the key with its private key
* Public/private key pairs are stored securely in PEM format on the Django server (inside the Python Docker container) and never in the database

**Secure Communication**

* HTTPS enabled using a self-signed certificate on the Nginx server
* Django is configured to only respond to HTTPS requests

---

