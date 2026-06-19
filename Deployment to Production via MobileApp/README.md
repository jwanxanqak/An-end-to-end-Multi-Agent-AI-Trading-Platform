# 📈 AlphaAgent — Multi-Agent Trading Mobile Application

[![FastAPI](https://img.shields.io/badge/Backend-FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![Streamlit](https://img.shields.io/badge/Frontend-Streamlit-FF4B4B?style=flat-square&logo=streamlit&logoColor=white)](https://streamlit.io/)
[![Deployment - Render](https://img.shields.io/badge/Deploy-Render-46E3B7?style=flat-square&logo=render&logoColor=white)](https://render.com/)
[![Python 3.11](https://img.shields.io/badge/Python-3.11-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)

# Mobile Architecture Deployment and Evolution Strategy

This document details the technical roadmap and implementations executed for the transition of the **AlphaAgent** platform from a desktop environment to native mobile ecosystems, ensuring high availability, resource optimization, and scalability in the user experience (UX).

---

## 🛠️ Implemented Architecture Approaches

The following describes the four phases of mobile optimization and packaging developed for the project:

### 1. Responsive Web Interface (Mobile-First)
* **Description:** Restructuring of the main graphical interface hosted on the Python/Streamlit backend, prioritizing an adaptive design focused on vertical screens.

* **Technical Components:** * Optimization of breakpoints and grids for the correct display of analytical data dashboards and market visualizations.

* Input of styles and viewport configurations adapted to mitigate visual latency in high-frequency mobile interactions.

* Usability-centric approach (UI/UX) to facilitate manipulation of the AI ​​agent control console from mobile devices.

### 2. PWA (Progressive Web App)
* **Description:** Evolution of the responsive website into a Progressive Web App to provide the platform with native capabilities directly from the device's browser (Safari, Chrome).

* **Technical Components:**

* **`manifest.json`:** Application manifest configuration to define high-resolution icons, fixed screen orientation, and standalone display modes (full screen without navigation bar).

* **Service Workers:** Caching architecture to optimize initial load times for static web resources.

* **Installability:** Cross-platform compatibility for direct addition to the operating system's home screen without app store intermediaries.

### 3. Native Container (WebView / Embedded Shell)
* **Description:** Encapsulation of the PWA in a lightweight native shell or ecosystem that acts as a direct bridge between the operating system and the remote execution backend.

* **Technical Components:**

* Use of automated cloud-based WebView engines to generate rapidly distributed binary packages (`.apk`).

* **Asynchronous Deployment:** "Live mirror" architecture that allows updating AI agent logic or data graphs on the server without requiring the end user to download a new version of the application.

* Bypassing critical local network dependencies through distributed builds on remote servers.

### 4. Hybrid/Native App (Flutter Engine in the Cloud)
* **Description:** Migration of the web architecture to a robust, cross-platform native container using the Flutter SDK, orchestrated entirely from cloud-based development environments (Google Project IDX).

* **Technical Components:**

* **`webview_flutter`:** Integration of the official high-performance plugin based on native hardware rendering for Android and iOS.

* **Complete Decoupling:** Isolation of the local runtime environment by using Linux containers in cloud environments, avoiding memory bottlenecks or connectivity latency (Gradle timeouts).

* **API Bridge Ready:** Scalable architecture ready for direct integration with advanced native device features such as biometric authentication (FaceID/Fingerprint) and a background push notification channel for critical agent alerts.

---

## 📈 Summary of Benefits of the Hybrid/Cloud Approach

1. **Resource Efficiency:** Zero hardware overhead on local development machines by delegating Gradle build cycles to the Google Cloud ecosystem.

2. **Modularity:** Clean separation between agent analytics logic in Python and rendering in the mobile layer.

3. **Cross-Platform Scalability:** Single codebase in Dart (`main.dart`) ready to scale to official distributions on the Google Play Store and Apple App Store.

## **Development environment**

<img width="795" height="631" alt="image" src="https://github.com/user-attachments/assets/269e9e46-c35a-488b-a105-7f7dd9604af4" />
<img width="796" height="637" alt="image" src="https://github.com/user-attachments/assets/271efcee-af68-4c9a-b77b-99f0acd6007c" />
<img width="797" height="639" alt="image" src="https://github.com/user-attachments/assets/d26203c4-9801-4a61-9879-aea970526e5b" />
<img width="797" height="648" alt="image" src="https://github.com/user-attachments/assets/eaad142c-b576-4eb5-a856-0465292dc01d" />
<img width="794" height="630" alt="image" src="https://github.com/user-attachments/assets/78ba8e75-1c7d-4397-a983-5bb53770f423" />

## **Production environment**
<img width="334" height="645" alt="image" src="https://github.com/user-attachments/assets/3ba36334-dbf2-4703-8e43-a73eea5d39a4" />
<img width="318" height="640" alt="image" src="https://github.com/user-attachments/assets/5932f093-62d3-43fb-83c0-eab940cb83d9" />
<img width="332" height="617" alt="image" src="https://github.com/user-attachments/assets/5ab90c5f-f4a0-4ef1-b3ab-fa7e97d40531" />
<img width="318" height="629" alt="image" src="https://github.com/user-attachments/assets/51d206c2-e5ea-4899-8e87-a6281a94742d" />
<img width="328" height="640" alt="image" src="https://github.com/user-attachments/assets/507e64b7-713e-44e3-84f6-730d6c20d3ba" />
<img width="329" height="632" alt="image" src="https://github.com/user-attachments/assets/5d16eef1-1cf0-4532-a61f-86adfc8188dc" />
<img width="316" height="625" alt="image" src="https://github.com/user-attachments/assets/c7730159-f84f-48c3-8fa1-76fbc115f719" />



