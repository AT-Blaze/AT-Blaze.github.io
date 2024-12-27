---
title: "Check your self..."
# url: "/12/Parker Chirps"
draft: false
---
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        #editable {
            border: 1px solid #ccc;
            padding: 10px;
            min-height: 150px;
            width: 100%;
            max-width: 800px;
            margin-bottom: 20px;
        }
        #metrics {
            font-size: 16px;
            background-color: #f9f9f9;
            padding: 10px;
            border: 1px solid #ddd;
            width: 100%;
            max-width: 800px;
        }
    </style>
</head>
<body>
    <h1></h1>
    <div id="editable" contenteditable="true">
        Type or paste text here to calculate readability metrics...
    </div>
    <div id="metrics">
        <strong>Metrics:</strong>
        <div id="fleschScore">Flesch Reading Ease: </div>
        <div id="gradeLevel">Grade Level: </div>
        <div id="wordsPerSentence">Words per Sentence: </div>
        <div id="syllablesPer100Words">Syllables per 100 Words: </div>
    </div>

   <script>
        function countSyllables(word) {
            word = word.toLowerCase();
            if (word.length <= 3) return 1;
            word = word.replace(/(?:[^laeiouy]es|ed|[^laeiouy]e)$/, '');
            word = word.replace(/^y/, '');
            const matches = word.match(/[aeiouy]{1,2}/g);
            return matches ? matches.length : 1;
        }

        function calculateMetrics(text) {
            const sentences = text.match(/[^.!?]+[.!?]+/g) || [text];
            const words = text.match(/\b\w+\b/g) || [];
            const syllables = words.reduce((count, word) => count + countSyllables(word), 0);

            const totalSentences = sentences.length;
            const totalWords = words.length;

            const wordsPerSentence = totalWords / totalSentences;
            const syllablesPer100Words = (syllables / totalWords) * 100;

            const fleschScore = 206.835 - (1.015 * wordsPerSentence) - (84.6 * (syllables / totalWords));

            const gradeLevel = (0.39 * wordsPerSentence) + (11.8 * (syllables / totalWords)) - 15.59;

            return {
                fleschScore: fleschScore.toFixed(2),
                gradeLevel: gradeLevel.toFixed(2),
                wordsPerSentence: wordsPerSentence.toFixed(2),
                syllablesPer100Words: syllablesPer100Words.toFixed(2)
            };
        }

        function updateMetrics() {
            const text = document.getElementById('editable').innerText;
            const metrics = calculateMetrics(text);

            document.getElementById('fleschScore').innerText = `Flesch Reading Ease: ${metrics.fleschScore}`;
            document.getElementById('gradeLevel').innerText = `Grade Level: ${metrics.gradeLevel}`;
            document.getElementById('wordsPerSentence').innerText = `Words per Sentence: ${metrics.wordsPerSentence}`;
            document.getElementById('syllablesPer100Words').innerText = `Syllables per 100 Words: ${metrics.syllablesPer100Words}`;
        }

        document.getElementById('editable').addEventListener('input', updateMetrics);

        // Initial calculation
        updateMetrics();
    </script>
![oops](/images/Flesch-Reading-Ease-Guide.png)
</body>
</html>
