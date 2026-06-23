<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>MATLAB Experiments PPT-1 Viewer</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
 
    body {
      font-family: 'Segoe UI', sans-serif;
      background: #1e1e2e;
      color: #cdd6f4;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
 
    header {
      width: 100%;
      background: #181825;
      padding: 14px 24px;
      display: flex;
      align-items: center;
      gap: 12px;
      border-bottom: 1px solid #313244;
      position: sticky;
      top: 0;
      z-index: 100;
    }
 
    header .icon {
      font-size: 22px;
    }
 
    header h1 {
      font-size: 16px;
      font-weight: 600;
      color: #cba6f7;
      flex: 1;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }
 
    .toolbar {
      display: flex;
      align-items: center;
      gap: 8px;
    }
 
    .toolbar button {
      background: #313244;
      border: none;
      color: #cdd6f4;
      padding: 6px 14px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 14px;
      transition: background 0.2s;
    }
 
    .toolbar button:hover { background: #45475a; }
    .toolbar button:disabled { opacity: 0.3; cursor: default; }
 
    .page-info {
      font-size: 13px;
      color: #a6adc8;
      min-width: 90px;
      text-align: center;
    }
 
    #zoom-select {
      background: #313244;
      border: none;
      color: #cdd6f4;
      padding: 6px 10px;
      border-radius: 6px;
      font-size: 13px;
      cursor: pointer;
    }
 
    #viewer-container {
      width: 100%;
      flex: 1;
      overflow-y: auto;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 24px 16px;
      gap: 16px;
    }
 
    .page-wrapper {
      position: relative;
      box-shadow: 0 4px 24px rgba(0,0,0,0.5);
      border-radius: 4px;
      overflow: hidden;
      background: white;
    }
 
    canvas {
      display: block;
    }
 
    #loading {
      margin-top: 80px;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 16px;
    }
 
    .spinner {
      width: 44px;
      height: 44px;
      border: 4px solid #313244;
      border-top-color: #cba6f7;
      border-radius: 50%;
      animation: spin 0.8s linear infinite;
    }
 
    @keyframes spin { to { transform: rotate(360deg); } }
 
    #loading p {
      color: #a6adc8;
      font-size: 14px;
    }
 
    #error-msg {
      display: none;
      margin-top: 60px;
      text-align: center;
      color: #f38ba8;
      font-size: 15px;
      max-width: 440px;
      line-height: 1.6;
    }
  </style>
</head>
<body>
 
<header>
  <span class="icon">📄</span>
  <h1>MATLAB Experiments PPT-1</h1>
  <div class="toolbar">
    <button id="prev-btn" disabled>◀ Prev</button>
    <span class="page-info" id="page-info">— / —</span>
    <button id="next-btn" disabled>Next ▶</button>
    <select id="zoom-select">
      <option value="0.75">75%</option>
      <option value="1.0" selected>100%</option>
      <option value="1.25">125%</option>
      <option value="1.5">150%</option>
      <option value="2.0">200%</option>
    </select>
  </div>
</header>
 
<div id="viewer-container">
  <div id="loading">
    <div class="spinner"></div>
    <p>Loading PDF…</p>
  </div>
  <div id="error-msg"></div>
</div>
 
<script>
  // Use a CORS proxy to load the PDF from GitHub raw
  const RAW_URL = "https://raw.githubusercontent.com/mrdren13-dot/mech2/22b4cad02baa927ed18275bdb8ffea482279efda/MATLAB%20Experiments%20PPT-1%20(1).pdf";
  const PROXY   = "https://corsproxy.io/?" + encodeURIComponent(RAW_URL);
 
  pdfjsLib.GlobalWorkerOptions.workerSrc =
    "https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js";
 
  let pdfDoc    = null;
  let pageNum   = 1;
  let scale     = 1.0;
  let rendering = false;
  let pending   = null;
 
  const container  = document.getElementById("viewer-container");
  const loading    = document.getElementById("loading");
  const errorMsg   = document.getElementById("error-msg");
  const pageInfo   = document.getElementById("page-info");
  const prevBtn    = document.getElementById("prev-btn");
  const nextBtn    = document.getElementById("next-btn");
  const zoomSelect = document.getElementById("zoom-select");
 
  async function renderPage(num) {
    rendering = true;
    const page = await pdfDoc.getPage(num);
    const viewport = page.getViewport({ scale });
 
    // Reuse or create canvas
    let wrapper = document.getElementById("page-" + num);
    if (!wrapper) {
      wrapper = document.createElement("div");
      wrapper.className = "page-wrapper";
      wrapper.id = "page-" + num;
      const canvas = document.createElement("canvas");
      wrapper.appendChild(canvas);
      container.appendChild(wrapper);
    }
 
    const canvas = wrapper.querySelector("canvas");
    const ctx = canvas.getContext("2d");
    canvas.width  = viewport.width;
    canvas.height = viewport.height;
 
    await page.render({ canvasContext: ctx, viewport }).promise;
 
    pageInfo.textContent = `${num} / ${pdfDoc.numPages}`;
    prevBtn.disabled = num <= 1;
    nextBtn.disabled = num >= pdfDoc.numPages;
 
    rendering = false;
    if (pending !== null) {
      renderPage(pending);
      pending = null;
    }
  }
 
  function queueRender(num) {
    if (rendering) { pending = num; }
    else { renderPage(num); }
  }
 
  function clearPages() {
    container.querySelectorAll(".page-wrapper").forEach(el => el.remove());
  }
 
  async function loadPDF(url) {
    try {
      const loadingTask = pdfjsLib.getDocument({ url, withCredentials: false });
      pdfDoc = await loadingTask.promise;
      loading.style.display = "none";
      await renderPage(1);
    } catch (err) {
      loading.style.display = "none";
      errorMsg.style.display = "block";
      errorMsg.innerHTML = `
        <strong>Could not load the PDF.</strong><br><br>
        This is usually a CORS issue when opening the file locally.<br>
        Try hosting the HTML on a web server, or open it via GitHub Pages.<br><br>
        <small style="color:#6c7086">${err.message}</small>
      `;
    }
  }
 
  prevBtn.addEventListener("click", () => {
    if (pageNum <= 1) return;
    pageNum--;
    clearPages();
    queueRender(pageNum);
  });
 
  nextBtn.addEventListener("click", () => {
    if (pageNum >= pdfDoc.numPages) return;
    pageNum++;
    clearPages();
    queueRender(pageNum);
  });
 
  zoomSelect.addEventListener("change", () => {
    scale = parseFloat(zoomSelect.value);
    clearPages();
    queueRender(pageNum);
  });
 
  loadPDF(PROXY);
</script>
</body>
</html>
 
