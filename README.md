
# 📍 Project Naksha

> **Interactive Geography for the Modern Student**  
> *Turning rote memorization into visual exploration.*

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![React](https://img.shields.io/badge/React-19-blue)
![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue)

## 📖 The Origin Story

The idea for **Naksha** was born out of personal necessity during my Class 10 academic year. Like millions of students preparing for board exams, I struggled with **Mapwork**.

Textbooks provided static, cluttered images. Online tutorials were low-resolution videos that didn't allow for hands-on practice. I realized that to truly master the geography of India—from the Nuclear Power Plants in the south to the Himalayan dams in the north—I needed to **interact** with the data, not just stare at it.

What started as a series of high-quality PDFs has evolved into this dynamic web application.

---

## ⚙️ The Engineering Journey & Challenges

Building a map app sounds simple until you refuse to use paid APIs (like Google Maps) to keep it educational and lightweight. I chose to build a **Custom SVG Engine**, which led to several unique engineering challenges.

### 1. The "AI Limitation" Discovery
I initially attempted to leverage modern AI (LLMs) to accelerate development, but I hit a hard wall regarding **Spatial Reasoning**:

*   **Generating the Map:** I asked current state-of-the-art models to "Generate an SVG map of India with state borders." The results were geometrically incoherent—blobs that looked nothing like the country. Current AI models struggle significantly with generating complex vector geometry code from scratch.
*   **Calibrating Coordinates:** I provided the AI with the SVG path data and asked it to "Calculate the X,Y coordinates for Mumbai." The models hallucinated wild coordinates that landed in the ocean or outside the viewport.

**Conclusion:** AI is excellent for logic, but currently fails at precise visual-spatial translation in code. I had to go manual.

### 2. The Calibration Challenge
The map operates on a massive coordinate space (`21000 x 29700` units). Mapping the syllabus locations (e.g., *Bhilai Steel Plant, Tehri Dam*) precisely on this grid was a laborious nightmare. Guessing coordinates, refreshing, and adjusting pixels took 5 minutes per location. With 50+ locations, this was unscalable.

### 3. The "Smart" Solution: Calibration Mode
To solve this, I engineered a temporary **Calibration Mode** within the app.
1.  I wrote a click listener that translated screen pixels into the SVG's matrix coordinate space.
2.  I clicked on the map visually where a city should be.
3.  The app logged the precise `{ x: 12340, y: 5500 }` object to the console.
4.  I simply copy-pasted these logs into my data file.

This tool reduced a 10-hour manual task into a 30-minute rapid-fire session, ensuring pixel-perfect accuracy for every dam, airport, and mine.

---

## 🚀 Key Features

*   **Vector Fidelity:** Uses a high-resolution SVG. Unlike JPGs, this map stays crisp at any zoom level.
*   **Interactive Viewport:** Custom implementation of Pan & Zoom logic with matrix transformations.
*   **Mobile Gestures:** Full support for pinch-to-zoom using `Math.hypot` calculations for touch events.
*   **Gamified Quiz:**
    *   Randomized location questioning.
    *   **Guidance Line:** If you click the wrong spot, a vector line draws a path from your mistake to the correct location, providing instant visual feedback.
*   **Procedural Audio:** No MP3 files. All sounds (success chimes, error buzzers) are synthesized in real-time using the **Web Audio API** oscillators to keep the app lightweight.

## 🛠️ Tech Stack

*   **Frontend:** React 18
*   **Language:** TypeScript
*   **Styling:** CSS Modules & Glassmorphism UI
*   **Graphics:** Inline SVG Manipulation
*   **State:** React Hooks (`useMemo`, `useCallback`)

## 🏃‍♂️ How to Run

1.  Clone the repository.
2.  Install dependencies:
    ```bash
    npm install
    ```
3.  Run the development server:
    ```bash
    npm run dev
    ```

## 👨‍💻 Author

**Pradumon Sahani**  
*Full Stack Developer & Security Researcher*

Created with ❤️ to make education free, accessible, and interactive.
