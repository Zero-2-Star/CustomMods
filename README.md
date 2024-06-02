# How to make mods?
Create a json file that becomes the base for the mode information and create a JavaScript file.

# mod.json
```json
{
    "cover": "https://example.com/cover.png",
    "favicon": "https://example.com/favicon.png",
    "title": {
        "en": "Example Mod",
        "ko": "예시용 모드",
        "ja": "例示用モード"
    },
    "language": "ko", // 2-letter language code
    "creators": ["Example1", "Example2"],
    "script": [
        "https://example.com/mod.js",
        "https://example.com/scene.js"
    ],
    "style": [
        "https://example.com/mod.css",
        "https://example.com/scene.css"
    ]
}
```

# mod.js
```javascript
(() => {
    // For your convenience, name and import the resource.
    Resource.register("image", "main", "https://example.com/image/main.png");
    Resource.register("image", "intro", "https://example.com/image/intro.png");
    Resource.register("audio", "main", "https://example.com/audio/main.mp3");

    Language.expand = [
        { "code": "ko", "url": "https://example.com/lang/ko.json" },
        { "code": "en", "url": "https://example.com/lang/en.json" },
        { "code": "ja", "url": "https://example.com/lang/ja.json" }
    ];
    Image.expand = Resource.getList("image");
    Audio.expand = Resource.getList("audio");
    Spacebar.expand = ["frame1", "frame2"];

    MainScene.backgroundPath = Resource.getUrl("image", "main");
    IntroScene.backgroundPath = Resource.getUrl("image", "intro");
    MainScene.audioPath = Resource.getUrl("audio", "main");
    MainScene.playMoveScene = "example";

    Scene.sceneExpand = (name) => {
        if (name == "example") {
            return getScene_example();
        }
    };

    Scene.frameExpand = (info, isSkip) => {
        let type = info["type"];
        let scene = Scene.getScene(Scene.sceneName);
        if (type == "customUI") {
            let newEl = document.createElement("div");
            newEl.classList.add("custom_ui");
            newEl.textContent = info["text"];
            scene.appendChild(newEl);
            isSkip = true;
        }
        return isSkip;
    };
})();

function getScene_example() {
    return [
        { "type": "customUI", "text": "Custom UI!" },
        { "type": "background", "color": "#000000" },
        { "type": "dialog", "text": "Hello World!", "location": "Empty place", "name": "Miraku", "color": "#ffffff" },
        { "type": "dialog", "text": "My name is Miraku!", "location": "Empty place", "name": "Miraku", "color": "#ffffff" }
    ];
}
```

# mod.css
```css
.custom_ui {
    width: 100%; height: 100%;
    position: absolute; color: #ffffff;
    font-size: calc(var(--gh) * 0.1);
}
```
