Yes, there are open-source music recognition models and frameworks available that you can use as a starting point for building your music recognition algorithm. Some of these models leverage deep learning techniques to achieve high accuracy in recognizing songs. Here are a few notable ones:

1. **ACRCloud:** ACRCloud offers an audio fingerprinting and recognition system that can be integrated into various applications. They provide SDKs for different programming languages that allow you to recognize songs based on short audio clips or streams. They offer both free and paid plans.
    
    Website: [https://www.acrcloud.com/](https://www.acrcloud.com/)
    
2. **Dejavu:** Dejavu is an open-source audio fingerprinting and recognition system written in Python. It allows you to build a database of audio fingerprints and then query it to recognize songs in audio recordings or streams. Dejavu is customizable and has a large community of contributors.
    
    GitHub Repository: [https://github.com/worldveil/dejavu](https://github.com/worldveil/dejavu)
    
3. **Essentia:** Essentia is an open-source library for audio analysis and music information retrieval. While not focused solely on music recognition, it provides various tools and algorithms that can be used for feature extraction, tempo estimation, and more, which are essential components of a music recognition system.
    
    GitHub Repository: [https://github.com/MTG/essentia](https://github.com/MTG/essentia)
    
4. **Musicnn:** Musicnn is a pre-trained deep learning model for music audio analysis. It can classify audio into various classes, including genres and moods. While it's not specifically designed for song recognition, you can potentially adapt its features for recognizing specific songs.
    
    GitHub Repository: [https://github.com/jordipons/musicnn](https://github.com/jordipons/musicnn)
    
5. **Chromaprint:** Chromaprint is a library for audio fingerprinting that uses chroma-based features to identify pieces of music. It's used in the AcoustID project, which is a collaborative music database used by music recognition applications.
    
    GitHub Repository: [https://github.com/acoustid/chromaprint](https://github.com/acoustid/chromaprint)
    

When using these open-source models, keep in mind that you may need to customize and extend them to meet your specific requirements. Additionally, integrating a music recognition system involves more than just the model itself – you'll need to handle audio input, preprocessing, and possibly integration with external APIs or databases for music metadata.