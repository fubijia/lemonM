<!doctype html>
<html lang="zh">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>AI助教</title>
  <style>
    * { box-sizing: border-box; }
    html, body { margin: 0; padding: 0; height: 100%; }
  </style>
</head>
<body>
  <iframe
    id="coze-web-sdk"
    src="https://sdk.coze.site"
    style="width: 100%; height: 100%; border: none;"
    allow="microphone;camera"
  ></iframe>

  <script>
    const cozeWebSDK = document.getElementById("coze-web-sdk");
    const COZE_WEB_SDK_ORIGIN = "https://sdk.coze.site";

    window.addEventListener("message", (event) => {
      // 只处理来自 SDK 的消息
      if (event.origin !== COZE_WEB_SDK_ORIGIN) {
        return;
      }
      const data = event.data;

      // SDK 准备就绪后，发送初始化指令
      if (data.type === "IFRAME_READY") {
        cozeWebSDK.contentWindow.postMessage({
          type: "INIT",
          payload: {
            // ← 把这里替换成你的 Token
            token: "pat_qa57qH9KpdGHmVg6JipqsN4c8STv7vcQUYXpFpANwZSsDtWknEnYHyMWtBA0VwW0",
            // ← 把这里替换成你的 Project ID
            projectId: "7643657850203602970"
          }
        }, COZE_WEB_SDK_ORIGIN);
      }

      // Token 过期时自动更新
      if (data.type === "TOKEN_EXPIRED") {
        cozeWebSDK.contentWindow.postMessage({
          type: "UPDATE_TOKEN",
          payload: {
            // ← 替换为新 Token（如果过期了的话）
            token: "pat_qa57qH9KpdGHmVg6JipqsN4c8STv7vcQUYXpFpANwZSsDtWknEnYHyMWtBA0VwW0"
          }
        }, COZE_WEB_SDK_ORIGIN);
      }
    });
  </script>
</body>
</html>
