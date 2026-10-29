
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="theme-color" content="#101827">
    <title>Fashion Visual Search System</title>

    <style>
        :root {
            --bg: #0b1120;
            --card: #151f32;
            --accent: #a78bfa;
            --text: #f1f5f9;
            --muted: #a5b4c8;
            --border: #29364d;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        html {
            scroll-behavior: smooth;
        }

        body {
            font-family: Arial, Helvetica, sans-serif;
            background: var(--bg);
            color: var(--text);
            line-height: 1.7;
        }

        a {
            color: #c4b5fd;
            text-decoration: none;
        }

        .container {
            width: min(1100px, 92%);
            margin: auto;
        }

        header {
            padding: 75px 0 55px;
            text-align: center;
            background:
                radial-gradient(ellipse at top, #35245f 0%, transparent 65%),
                var(--bg);
            border-bottom: 1px solid var(--border);
        }

        .tag {
            display: inline-block;
            padding: 7px 14px;
            border: 1px solid #6854a3;
            border-radius: 30px;
            color: #ddd6fe;
            font-size: 13px;
            margin-bottom: 22px;
        }

        h1 {
            font-size: clamp(30px, 5vw, 48px);
            line-height: 1.2;
            letter-spacing: -1px;
            margin-bottom: 20px;
        }

        h1 span {
            color: var(--accent);
        }

        .subtitle {
            max-width: 700px;
            margin: 0 auto 28px;
            color: var(--muted);
            font-size: 17px;
        }

        .buttons {
            display: flex;
            justify-content: center;
            gap: 12px;
            flex-wrap: wrap;
        }

        .btn {
            padding: 11px 20px;
            border-radius: 9px;
            font-weight: bold;
            background: var(--accent);
            color: #17102c;
            transition: 0.2s;
        }

        .btn:hover {
            transform: translateY(-2px);
            opacity: 0.9;
        }

        .btn.secondary {
            color: var(--text);
            background: var(--card);
            border: 1px solid var(--border);
        }

        nav {
            position: sticky;
            top: 0;
            z-index: 10;
            background: rgba(11, 17, 32, 0.96);
            border-bottom: 1px solid var(--border);
            padding: 13px 0;
        }

        .nav-links {
            display: flex;
            justify-content: center;
            gap: 22px;
            flex-wrap: wrap;
            font-size: 14px;
        }

        main {
            padding: 35px 0 65px;
        }

        section {
            margin: 30px 0 45px;
            scroll-margin-top: 75px;
        }

        h2 {
            font-size: 25px;
            margin-bottom: 17px;
        }

        h2::before {
            content: "";
            display: inline-block;
            width: 5px;
            height: 24px;
            background: var(--accent);
            border-radius: 5px;
            margin-right: 11px;
            vertical-align: -4px;
        }

        p {
            color: var(--muted);
            margin-bottom: 13px;
        }

        .grid {
            display: grid;
            grid-template-columns:
                repeat(auto-fit, minmax(220px, 1fr));
            gap: 17px;
        }

        .card {
            background: var(--card);
            border: 1px solid var(--border);
            border-radius: 14px;
            padding: 23px;
            transition: border-color 0.2s,
                        transform 0.2s;
        }

        .card:hover {
            border-color: #8066cb;
            transform: translateY(-3px);
        }

        .icon {
            font-size: 28px;
            margin-bottom: 12px;
        }

        h3 {
            font-size: 17px;
            margin-bottom: 9px;
        }

        .card p {
            font-size: 14px;
            margin-bottom: 0;
        }

        .steps {
            counter-reset: step;
            display: grid;
            gap: 14px;
        }

        .step {
            display: flex;
            gap: 16px;
            align-items: flex-start;
            background: var(--card);
            border: 1px solid var(--border);
            padding: 19px;
            border-radius: 12px;
        }

        .number {
            flex-shrink: 0;
            display: grid;
            place-items: center;
            width: 36px;
            height: 36px;
            border-radius: 10px;
            background: #30234f;
            color: #ddd6fe;
            font-weight: bold;
        }

        .step p {
            margin: 0;
            font-size: 14px;
        }

        .tech-list {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
        }

        .tech {
            background: #1b2940;
            border: 1px solid var(--border);
            border-radius: 8px;
            padding: 8px 13px;
            font-size: 14px;
        }

        pre {
            background: #080d18;
            color: #dbeafe;
            border: 1px solid var(--border);
            padding: 18px;
            border-radius: 12px;
            overflow-x: auto;
            margin: 14px 0;
            font-size: 14px;
        }

        .note {
            padding: 17px;
            border-left: 4px solid var(--accent);
            background: #17182c;
            border-radius: 0 10px 10px 0;
        }

        footer {
            text-align: center;
            padding: 30px 15px;
            border-top: 1px solid var(--border);
            color: var(--muted);
            font-size: 13px;
        }

        @media (max-width: 600px) {
            header {
                padding: 48px 0 40px;
            }

            .nav-links {
                gap: 12px;
                font-size: 12px;
            }

            .card {
                padding: 18px;
            }

            h2 {
                font-size: 22px;
            }
        }
    </style>
</head>

<body>

<header>
    <div class="container">
        <div class="tag">DEEP LEARNING · COMPUTER VISION</div>

        <h1>
            Fashion <span>Visual Search</span><br>
            System
        </h1>

        <p class="subtitle">
            Discover visually similar fashion products using
            deep learning, ResNet50 feature extraction,
            and intelligent similarity matching.
        </p>

        <div class="buttons">
            <a class="btn" href="#about">Explore Project ↓</a>
            <a class="btn secondary"
               href="https://github.com/"
               target="_blank" rel="noopener">
                GitHub
            </a>
        </div>
    </div>
</header>

<nav>
    <div class="container nav-links">
        <a href="#about">About</a>
        <a href="#features">Features</a>
        <a href="#workflow">Workflow</a>
        <a href="#technology">Technology</a>
        <a href="#installation">Setup</a>
        <a href="#future">Future Scope</a>
    </div>
</nav>

<main class="container">

    <section id="about">
        <h2>About the Project</h2>

        <p>
            The Deep Learning Based Fashion Visual Search System
            is designed to retrieve visually similar fashion
            products from a collection of images.
        </p>

        <p>
            Instead of relying only on text-based searches,
            the system extracts visual features from images
            using a pretrained ResNet50 model. It compares
            these features using cosine similarity and can
            apply metadata filtering to refine the results.
        </p>

        <div class="note">
            <strong>Project objective</strong>
            <p>
                Make fashion product discovery easier by finding
                visually similar items from an image.
            </p>
        </div>
    </section>

    <section id="features">
        <h2>Key Features</h2>

        <div class="grid">
            <div class="card">
                <div class="icon">🧠</div>
                <h3>Deep Feature Extraction</h3>
                <p>
                    Uses pretrained ResNet50 to extract meaningful
                    visual representations of fashion images.
                </p>
            </div>

            <div class="card">
                <div class="icon">🔎</div>
                <h3>Visual Search</h3>
                <p>
                    Finds products with visual characteristics
                    similar to a query image.
                </p>
            </div>

            <div class="card">
                <div class="icon">📐</div>
                <h3>Cosine Similarity</h3>
                <p>
                    Measures similarity between feature vectors
                    to rank candidate products.
                </p>
            </div>

            <div class="card">
                <div class="icon">🏷️</div>
                <h3>Metadata Filtering</h3>
                <p>
                    Uses available product metadata to narrow
                    the search results where applicable.
                </p>
            </div>

            <div class="card">
                <div class="icon">👕</div>
                <h3>Top-5 Retrieval</h3>
                <p>
                    Retrieves the five highest-ranked matching
                    products from the search collection.
                </p>
            </div>

            <div class="card">
                <div class="icon">⚡</div>
                <h3>Automated Processing</h3>
                <p>
                    Processes image features and similarity
                    calculations using Python libraries.
                </p>
            </div>
        </div>
    </section>

    <section id="workflow">
        <h2>How It Works</h2>

        <div class="steps">
            <div class="step">
                <div class="number">01</div>
                <div>
                    <h3>Dataset Preparation</h3>
                    <p>
                        Load fashion images and their associated
                        metadata into the system.
                    </p>
                </div>
            </div>

            <div class="step">
                <div class="number">02</div>
                <div>
                    <h3>Feature Extraction</h3>
                    <p>
                        Use ResNet50 to convert images into
                        numerical feature vectors.
                    </p>
                </div>
            </div>

            <div class="step">
                <div class="number">03</div>
                <div>
                    <h3>Query Image Processing</h3>
                    <p>
                        Extract features from the image supplied
                        for the visual search.
                    </p>
                </div>
            </div>

            <div class="step">
                <div class="number">04</div>
                <div>
                    <h3>Similarity Ranking</h3>
                    <p>
                        Compare the query features with stored
                        features using cosine similarity.
                    </p>
                </div>
            </div>

            <div class="step">
                <div class="number">05</div>
                <div>
                    <h3>Display Results</h3>
                    <p>
                        Apply applicable metadata filters and
                        retrieve the top five matching products.
                    </p>
                </div>
            </div>
        </div>
    </section>

    <section id="technology">
        <h2>Technology Stack</h2>

        <p>
            The project combines deep learning, image processing,
            and data analysis tools.
        </p>

        <div class="tech-list">
            <span class="tech">Python</span>
            <span class="tech">TensorFlow</span>
            <span class="tech">ResNet50</span>
            <span class="tech">NumPy</span>
            <span class="tech">Pandas</span>
            <span class="tech">Scikit-learn</span>
            <span class="tech">Matplotlib</span>
            <span class="tech">Pillow</span>
            <span class="tech">KaggleHub</span>
        </div>
    </section>

    <section id="installation">
        <h2>Getting Started</h2>

        <h3>1. Clone the Repository</h3>
        <pre><code>git clone YOUR_REPOSITORY_URL
cd YOUR_PROJECT_FOLDER</code></pre>

        <h3>2. Install Dependencies</h3>
        <pre><code>pip install tensorflow scikit-learn pandas matplotlib pillow tqdm kagglehub</code></pre>

        <h3>3. Run the Project</h3>
        <p>
            Open the project notebook in Jupyter Notebook
            or Google Colab, configure the dataset path,
            and execute the cells in order.
        </p>

        <pre><code>jupyter notebook</code></pre>

        <p>
            Replace the repository URL and folder name above
            with your actual GitHub repository details.
        </p>
    </section>

    <section id="future">
        <h2>Future Enhancements</h2>

        <div class="grid">
            <div class="card">
                <h3>🌐 Web Interface</h3>
                <p>
                    Build an interactive interface for uploading
                    images and browsing search results.
                </p>
            </div>

            <div class="card">
                <h3>🎯 Improved Ranking</h3>
                <p>
                    Explore additional ranking methods and
                    evaluate retrieval quality.
                </p>
            </div>

            <div class="card">
                <h3>📱 Mobile Support</h3>
                <p>
                    Develop a responsive experience for
                    fashion searches on mobile devices.
                </p>
            </div>
        </div>
    </section>

    <section id="conclusion">
        <h2>Conclusion</h2>

        <p>
            This project demonstrates how deep learning can
            support content-based fashion image retrieval.
            By combining ResNet50 feature extraction, cosine
            similarity, and metadata filtering, it provides
            a foundation for building an intelligent fashion
            discovery application.
        </p>
    </section>

</main>

<footer>
    <p>
        Deep Learning Based Fashion Visual Search System
    </p>
    <p>Built with Python, TensorFlow and ResNet50</p>
</footer>

</body>
</html>
