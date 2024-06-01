# How to make mods?
Create a json file that becomes the base for the mode information and create a JavaScript file.

# mod.json
```json
{
    "cover": "https://example.com/cover.png",
    "title": {
        "en": "Example Mod",
        "ko": "예시용 모드",
        "ja": "例示用モード"
    },
    "language": "ko", // 2-letter language code
    "creators": ["Example1", "Example2"],
    "script": [
        "https://example.com/core.js",
        "https://example.com/scene.js"
    ],
    "style": [
        "https://example.com/core.css",
        "https://example.com/scene.css"
    ]
}
```
