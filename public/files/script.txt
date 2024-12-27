// ==UserScript==
// @name         Readability Metrics for Textarea and Body
// @namespace    http://tampermonkey.net/
// @version      1.1
// @description  Calculates readability metrics for text on the page and from a specific textarea
// @author       Antranig Douglas
// @match        *://*/*
// @grant        none
// ==/UserScript==

(function () {
    'use strict';

    // Utility function to count syllables in a word
    function countSyllables(word) {
        word = word.toLowerCase();
        if (word.length <= 3) return 1; // Short words typically have one syllable
        word = word.replace(/(?:[^laeiouy]es|ed|[^laeiouy]e)$/, '');
        word = word.replace(/^y/, '');
        const matches = word.match(/[aeiouy]{1,2}/g);
        return matches ? matches.length : 1;
    }

    // Function to calculate readability metrics
    function calculateMetrics(text) {
        const sentences = text.match(/[^.!?]+[.!?]+/g) || [text];
        const words = text.match(/\b\w+\b/g) || [];
        const syllables = words.reduce((count, word) => count + countSyllables(word), 0);

        const totalSentences = sentences.length;
        const totalWords = words.length;

        const wordsPerSentence = totalWords / totalSentences;
        const syllablesPer100Words = (syllables / totalWords) * 100;

        // Flesch reading ease score
        const fleschScore = 206.835 - (1.015 * wordsPerSentence) - (84.6 * (syllables / totalWords));

        return {
            fleschScore: fleschScore.toFixed(2),
            wordsPerSentence: wordsPerSentence.toFixed(2),
            syllablesPer100Words: syllablesPer100Words.toFixed(2),
        };
    }

    // Function to create and display the metrics box
    function createMetricsBox(metrics) {
        const metricsBox = document.createElement('div');
        metricsBox.style.position = 'fixed';
        metricsBox.style.bottom = '10px';
        metricsBox.style.right = '10px';
        metricsBox.style.padding = '10px';
        metricsBox.style.backgroundColor = 'rgba(0, 0, 0, 0.8)';
        metricsBox.style.color = 'white';
        metricsBox.style.borderRadius = '5px';
        metricsBox.style.fontSize = '14px';
        metricsBox.style.zIndex = '10000';
        metricsBox.style.border = '2px solid red'; // Debug styling

        // Safely set innerHTML to avoid errors
        const safeMetrics = {
            fleschScore: metrics.fleschScore || 'N/A',
            wordsPerSentence: metrics.wordsPerSentence || 'N/A',
            syllablesPer100Words: metrics.syllablesPer100Words || 'N/A',
        };

        try {
            metricsBox.innerHTML = `
                <strong>Readability Metrics</strong><br>
                Flesch Score: ${safeMetrics.fleschScore}<br>
                Words per Sentence: ${safeMetrics.wordsPerSentence}<br>
                Syllables per 100 Words: ${safeMetrics.syllablesPer100Words}
            `;
            document.body.appendChild(metricsBox);
            console.log('Metrics box successfully appended:', safeMetrics);
        } catch (e) {
            console.error('Error rendering metrics box:', e);
        }
    }

    // Extract text content from the page
    function getPageText() {
        const textarea = document.querySelector('#textbox');
        const textareaText = textarea ? textarea.value : '';
        const bodyText = document.body.innerText || '';
        return `${textareaText}\n${bodyText}`.trim();
    }

    // Main execution
    try {
        const pageText = getPageText();
        console.log('Extracted text:', pageText);

        const metrics = calculateMetrics(pageText);
        console.log('Calculated metrics:', metrics);

        createMetricsBox(metrics);
    } catch (error) {
        console.error('Error during script execution:', error);
    }
})();