<!-- 引入 FontAwesome 企業圖示庫 -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

<style>
  /* 深色企業內頁全域樣式 */
  .enterprise-page {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
    color: #f8fafc;
    padding: 10px 0;
  }

  /* 頂部導覽列與標題 */
  .top-nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
  }

  .btn-back {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: #1e293b;
    border: 1px solid #334155;
    color: #38bdf8;
    padding: 8px 16px;
    border-radius: 8px;
    text-decoration: none;
    font-size: 14px;
    font-weight: 500;
    transition: all 0.2s;
  }

  .btn-back:hover {
    background: #334155;
    border-color: #38bdf8;
    color: #ffffff;
  }

  .badge-confidential {
    background: rgba(239, 68, 68, 0.15);
    color: #ef4444;
    border: 1px solid rgba(239, 68, 68, 0.3);
    padding: 4px 10px;
    border-radius: 20px;
    font-size: 12px;
    font-weight: 700;
    letter-spacing: 0.5px;
  }

  .page-title {
    font-size: 24px;
    font-weight: 700;
    color: #f1f5f9;
    margin: 10px 0 20px 0;
    display: flex;
    align-items: center;
    gap: 12px;
  }

  /* 數據核心指標區塊 (Metric Cards) */
  .metrics-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 16px;
    margin-bottom: 25px;
  }

  .metric-card {
    background: #1e293b;
    border: 1px solid #334155;
    border-radius: 12px;
    padding: 18px;
  }

  .metric-header {
    font-size: 13px;
    color: #94a3b8;
    margin-bottom: 8px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .metric-value {
    font-size: 22px;
    font-weight: 700;
    color: #38bdf8;
    margin-bottom: 6px;
  }

  .metric-sub {
    font-size: 12px;
    color: #10b981;
    display: flex;
    align-items: center;
    gap: 4px;
  }

  /* 區塊面板 (Section Cards) */
  .panel-card {
    background: #1e293b;
    border: 1px solid #334155;
    border-radius: 12px;
    padding: 20px;
    margin-bottom: 25px;
  }

  .panel-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 15px;
  }

  .panel-title {
    font-size: 16px;
    font-weight: 600;
    color: #e2e8f0;
    margin: 0;
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .key-notes-list {
    margin: 0;
    padding-left: 20px;
    color: #cbd5e1;
    line-height: 1.7;
    font-size: 14px;
  }

  .key-notes-list li {
    margin-bottom: 8px;
  }

  /* PPT 簡報播放按鈕樣式 */
  .btn-ppt-present {
    background: linear-gradient(135deg, #0284c7, #2563eb);
    color: #ffffff;
    border: none;
    padding: 8px 18px;
    border-radius: 8px;
    font-size: 14px;
    font-weight: 600;
    cursor: pointer;
    display: inline-flex;
    align-items: center;
    gap: 8px;
    box-shadow: 0 4px 12px rgba(2, 132, 199, 0.3);
    transition: all 0.2s ease;
  }

  .btn-ppt-present:hover {
    background: linear-gradient(135deg, #0369a1, #1d4ed8);
    transform: translateY(-2px);
    box-shadow: 0 6px 16px rgba(2, 132, 199, 0.5);
  }

  /* PDF Preview Frame 包裹容器 */
  .pdf-container {
    width: 100%;
    border-radius: 8px;
    overflow: hidden;
    border: 1px solid #475569;
    background: #0f172a;
    transition: all 0.3s ease;
  }

  /* 當進入全螢幕簡報模式時的滿版樣式 */
  .pdf-container:fullscreen {
    width: 100vw !important;
    height: 100vh !important;
    border: none !important;
    border-radius: 0 !important;
    background: #000000 !important;
  }

  .pdf-container:-webkit-full-screen {
    width: 100vw !important;
    height: 100vh !important;
    border: none !important;
    border-radius: 0 !important;
    background: #000000 !important;
  }

  iframe {
    width: 100%;
    height: 700px;
    border: none;
    display: block;
  }

  .pdf-container:fullscreen iframe,
  .pdf-container:-webkit-full-screen iframe {
    height: 100vh !important;
  }
</style>

<div class="enterprise-page">

  <!-- 頂部導覽列 -->
  <div class="top-nav">
    <a href="./" class="btn-back">
      <i class="fa-solid fa-arrow-left"></i> Back to Archive
    </a>
    <span class="badge-confidential"><i class="fa-solid fa-lock"></i> RESTRICTED ACCESS</span>
  </div>

  <!-- 主標題 -->
  <div class="page-title">
    <i class="fa-solid fa-chart-line" style="color: #38bdf8;"></i>
    AMAT ENP Expansion & Capacity Report 2026
  </div>

  <!-- 數據重點指標面板 -->
  <div class="metrics-grid">
    <div class="metric-card">
      <div class="metric-header">
        <span>Target Capacity (Before)</span>
        <i class="fa-solid fa-industry" style="color: #94a3b8;"></i>
      </div>
      <div class="metric-value">2,592 PCS</div>
      <div class="metric-sub">
        <i class="fa-solid fa-gauge"></i> Est. Output @80%: 2,070 PCS/yr
      </div>
    </div>

    <div class="metric-card" style="border-color: #0284c7;">
      <div class="metric-header">
        <span>Post-Expansion Capacity</span>
        <i class="fa-solid fa-rocket" style="color: #38bdf8;"></i>
      </div>
      <div class="metric-value" style="color: #10b981;">4,032 PCS</div>
      <div class="metric-sub" style="color: #10b981;">
        <i class="fa-solid fa-arrow-trend-up"></i> Est. Output @80%: 3,225 PCS/yr (+55.8%)
      </div>
    </div>
  </div>

  <!-- Key Notes 說明區塊 -->
  <div class="panel-card">
    <div class="panel-header">
      <div class="panel-title">
        <i class="fa-solid fa-list-check" style="color: #38bdf8;"></i> Key Capacity Metrics & Highlights
      </div>
    </div>
    <ul class="key-notes-list">
      <li><b>2026 Before Expansion Target</b>: Max capacity of 2,592 PCS. At 80% utilization, estimated output is 2,070 PCS/year (min).</li>
      <li><b>2026 Post-Expansion (Auto Pretreatment + 2 Tanks)</b>: Max capacity of 4,032 PCS. At 80% utilization, estimated output is 3,225 PCS/year (min).</li>
    </ul>
  </div>

  <!-- PDF 簡報預覽面板（含 PPT 簡報播放按鈕） -->
  <div class="panel-card">
    <div class="panel-header">
      <div class="panel-title">
        <i class="fa-solid fa-file-pdf" style="color: #ef4444;"></i> Executive Presentation
      </div>
      <!-- PPT 滿版簡報播放按鈕 -->
      <button type="button" class="btn-ppt-present" onclick="startPPTPresentation()">
        <i class="fa-solid fa-play"></i> Start Presentation (全螢幕簡報)
      </button>
    </div>
    <div class="pdf-container" id="pdf-wrapper">
      <iframe id="pdf-frame" src="ENP_Expansion_Feedback%202026.pdf#view=Fit&pagemode=thumbs" allowfullscreen></iframe>
    </div>
  </div>

</div>

<!-- PPT 全螢幕簡報播放腳本 -->
<script>
  function startPPTPresentation() {
    const pdfWrapper = document.getElementById('pdf-wrapper');
    
    if (!document.fullscreenElement) {
      if (pdfWrapper.requestFullscreen) {
        pdfWrapper.requestFullscreen();
      } else if (pdfWrapper.webkitRequestFullscreen) { /* Safari */
        pdfWrapper.webkitRequestFullscreen();
      } else if (pdfWrapper.msRequestFullscreen) { /* IE11 */
        pdfWrapper.msRequestFullscreen();
      }
    } else {
      if (document.exitFullscreen) {
        document.exitFullscreen();
      }
    }
  }
</script>
