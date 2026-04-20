[ecotrack (4).html](https://github.com/user-attachments/files/26898616/ecotrack.4.html)
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>EcoTrack – Smart Plastic Waste Management</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet"/>
  <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet"/>
  <style>
    *,*::before,*::after{margin:0;padding:0;box-sizing:border-box}
    :root{
      --green-dark:#1a5c38;--green-mid:#27ae60;--green-light:#52c97e;--green-pale:#d4f5e2;
      --accent:#f0c040;--accent2:#3ecfcf;--bg:#0d1f16;--bg2:#112318;
      --glass:rgba(255,255,255,0.06);--glass-border:rgba(255,255,255,0.13);
      --text:#e8f5ee;--muted:#8db8a0;--card-bg:rgba(30,70,45,0.55);
      --radius:16px;--shadow:0 8px 32px rgba(0,0,0,0.38);--transition:0.3s cubic-bezier(.4,0,.2,1)
    }
    html,body{height:100%;width:100%;font-family:'Inter',sans-serif;background:var(--bg);color:var(--text);overflow:hidden}
    .bg-blobs{position:fixed;inset:0;z-index:0;overflow:hidden;pointer-events:none}
    .blob{position:absolute;border-radius:50%;filter:blur(80px);opacity:0.18;animation:blobMove 12s ease-in-out infinite alternate}
    .blob1{width:500px;height:500px;background:var(--green-mid);top:-120px;left:-100px;animation-delay:0s}
    .blob2{width:400px;height:400px;background:var(--accent2);bottom:-100px;right:-80px;animation-delay:4s}
    .blob3{width:300px;height:300px;background:var(--accent);top:40%;left:45%;animation-delay:2s}
    @keyframes blobMove{0%{transform:translate(0,0) scale(1)}100%{transform:translate(40px,30px) scale(1.08)}}
    /* AUTH */
    #authScreen{position:fixed;inset:0;z-index:1000;display:flex;align-items:center;justify-content:center;background:linear-gradient(135deg,#0b1a10 0%,#0d2c18 100%)}
    .auth-box{background:rgba(20,55,32,0.72);border:1px solid var(--glass-border);backdrop-filter:blur(22px);border-radius:24px;padding:44px 48px;width:420px;box-shadow:var(--shadow);position:relative;z-index:2}
    .auth-logo{text-align:center;margin-bottom:28px}
    .auth-logo .logo-icon{font-size:2.8rem;color:var(--green-light);display:block}
    .auth-logo h1{font-size:1.8rem;font-weight:800;letter-spacing:-0.5px;background:linear-gradient(90deg,var(--green-light),var(--accent2));-webkit-background-clip:text;-webkit-text-fill-color:transparent}
    .auth-logo p{color:var(--muted);font-size:0.85rem;margin-top:4px}
    .auth-tabs{display:flex;gap:8px;margin-bottom:28px;background:rgba(0,0,0,0.25);border-radius:10px;padding:4px}
    .auth-tab{flex:1;padding:9px;border:none;border-radius:8px;background:transparent;color:var(--muted);font-size:0.9rem;font-weight:600;cursor:pointer;transition:var(--transition)}
    .auth-tab.active{background:var(--green-mid);color:#fff}
    .auth-form{display:flex;flex-direction:column;gap:16px}
    .form-group label{font-size:0.82rem;font-weight:600;color:var(--muted);display:block;margin-bottom:6px;letter-spacing:.5px;text-transform:uppercase}
    .form-group input{width:100%;padding:11px 14px;border-radius:10px;border:1px solid var(--glass-border);background:rgba(255,255,255,0.06);color:var(--text);font-size:0.92rem;outline:none;transition:var(--transition)}
    .form-group input:focus{border-color:var(--green-light);background:rgba(255,255,255,0.1)}
    .auth-btn{width:100%;padding:13px;border:none;border-radius:12px;background:linear-gradient(135deg,var(--green-mid),var(--green-light));color:#fff;font-size:1rem;font-weight:700;cursor:pointer;transition:var(--transition);margin-top:4px;box-shadow:0 4px 18px rgba(39,174,96,0.35)}
    .auth-btn:hover{transform:translateY(-2px);box-shadow:0 8px 28px rgba(39,174,96,0.5)}
    .auth-error{color:#ff6b6b;font-size:0.83rem;text-align:center;min-height:18px;margin-top:-6px}
    .auth-quote{text-align:center;margin-top:22px;color:var(--muted);font-size:0.8rem;font-style:italic}
    /* APP */
    #app{display:none;height:100vh;width:100vw;flex-direction:column;position:relative;z-index:1}
    #app.visible{display:flex}
    /* NAVBAR */
    nav{height:62px;background:rgba(13,31,22,0.88);backdrop-filter:blur(18px);border-bottom:1px solid var(--glass-border);display:flex;align-items:center;padding:0 18px;flex-shrink:0;gap:4px;position:relative;z-index:50}
    .nav-brand{display:flex;align-items:center;gap:9px;margin-right:14px;text-decoration:none;cursor:pointer}
    .nav-brand .leaf{color:var(--green-light);font-size:1.3rem}
    .nav-brand span{font-size:1.1rem;font-weight:800;letter-spacing:-0.3px;background:linear-gradient(90deg,var(--green-light),var(--accent2));-webkit-background-clip:text;-webkit-text-fill-color:transparent}
    .nav-links{display:flex;align-items:center;gap:1px;flex:1;overflow-x:auto}
    .nav-links::-webkit-scrollbar{display:none}
    .nav-btn{padding:6px 10px;border:none;border-radius:9px;background:transparent;color:var(--muted);font-size:0.78rem;font-weight:500;cursor:pointer;transition:var(--transition);display:flex;align-items:center;gap:5px;white-space:nowrap}
    .nav-btn i{font-size:0.72rem}
    .nav-btn:hover{background:rgba(255,255,255,0.07);color:var(--text)}
    .nav-btn.active{background:rgba(39,174,96,0.22);color:var(--green-light);font-weight:600}
    .nav-right{display:flex;align-items:center;gap:10px;margin-left:auto;flex-shrink:0}
    .nav-credits{display:flex;align-items:center;gap:7px;background:rgba(240,192,64,0.15);border:1px solid rgba(240,192,64,0.3);border-radius:20px;padding:5px 12px;font-size:0.8rem;font-weight:700;color:var(--accent)}
    .nav-user-avatar{width:32px;height:32px;border-radius:50%;background:linear-gradient(135deg,var(--green-mid),var(--accent2));display:flex;align-items:center;justify-content:center;font-weight:700;font-size:0.82rem;color:#fff;cursor:pointer;flex-shrink:0}
    .logout-btn{padding:6px 10px;border-radius:8px;border:1px solid rgba(255,100,100,0.3);background:transparent;color:#ff8080;font-size:0.75rem;cursor:pointer;transition:var(--transition);flex-shrink:0}
    .logout-btn:hover{background:rgba(255,100,100,0.12)}
    /* CONTENT */
    #content{flex:1;overflow:hidden;position:relative}
    .section{display:none;position:absolute;inset:0;padding:24px 32px;animation:fadeIn 0.35s ease;overflow-y:auto;overflow-x:hidden}
    .section.active{display:block}
    @keyframes fadeIn{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:translateY(0)}}
    .section::-webkit-scrollbar{width:5px}
    .section::-webkit-scrollbar-track{background:transparent}
    .section::-webkit-scrollbar-thumb{background:var(--green-dark);border-radius:6px}
    /* COMPONENTS */
    .card{background:var(--card-bg);border:1px solid var(--glass-border);backdrop-filter:blur(12px);border-radius:var(--radius);padding:22px;box-shadow:var(--shadow)}
    .section-title{font-size:1.5rem;font-weight:800;margin-bottom:5px;background:linear-gradient(90deg,var(--green-light),var(--accent2));-webkit-background-clip:text;-webkit-text-fill-color:transparent}
    .section-sub{color:var(--muted);font-size:0.86rem;margin-bottom:22px}
    .badge{display:inline-block;padding:3px 10px;border-radius:20px;font-size:0.72rem;font-weight:700;letter-spacing:.5px}
    .badge-green{background:rgba(39,174,96,0.2);color:var(--green-light);border:1px solid rgba(82,201,126,0.3)}
    .badge-gold{background:rgba(240,192,64,0.2);color:var(--accent);border:1px solid rgba(240,192,64,0.3)}
    .eco-quote{text-align:center;padding:12px 18px;background:rgba(39,174,96,0.08);border:1px solid rgba(82,201,126,0.2);border-radius:12px;font-size:0.84rem;color:var(--muted);font-style:italic;margin-bottom:20px}
    .eco-quote span{color:var(--green-light);font-weight:600}
    .btn-primary{padding:11px 24px;border:none;border-radius:12px;background:linear-gradient(135deg,var(--green-mid),var(--green-light));color:#fff;font-size:0.92rem;font-weight:700;cursor:pointer;transition:var(--transition);box-shadow:0 4px 18px rgba(39,174,96,0.3)}
    .btn-primary:hover{transform:translateY(-2px);box-shadow:0 8px 28px rgba(39,174,96,0.45)}
    .btn-outline{padding:11px 24px;border:2px solid var(--green-mid);border-radius:12px;background:transparent;color:var(--green-light);font-size:0.92rem;font-weight:700;cursor:pointer;transition:var(--transition)}
    .btn-outline:hover{background:rgba(39,174,96,0.12)}
    .progress-bar{background:rgba(255,255,255,0.08);border-radius:20px;height:8px;overflow:hidden}
    .progress-fill{height:100%;border-radius:20px;background:linear-gradient(90deg,var(--green-mid),var(--green-light));transition:width 0.8s ease}
    .flex-between{display:flex;align-items:center;justify-content:space-between}
    /* HOME */
    #home{display:flex;flex-direction:column;justify-content:center;align-items:center;text-align:center;min-height:calc(100vh - 62px);padding:30px}
    #home.active{display:flex}
    .home-hero-icon{font-size:4.5rem;margin-bottom:14px;animation:float 3s ease-in-out infinite}
    @keyframes float{0%,100%{transform:translateY(0)}50%{transform:translateY(-12px)}}
    .home-title{font-size:3rem;font-weight:900;line-height:1.15;background:linear-gradient(135deg,#52c97e,#3ecfcf,#f0c040);-webkit-background-clip:text;-webkit-text-fill-color:transparent;margin-bottom:12px}
    .home-sub{font-size:1rem;color:var(--muted);max-width:520px;line-height:1.65;margin-bottom:28px}
    .home-btns{display:flex;gap:12px;flex-wrap:wrap;justify-content:center}
    .home-stats{display:flex;gap:16px;margin-top:36px;flex-wrap:wrap;justify-content:center}
    .home-stat{background:var(--card-bg);border:1px solid var(--glass-border);backdrop-filter:blur(10px);border-radius:14px;padding:16px 24px;text-align:center}
    .home-stat .val{font-size:1.6rem;font-weight:800;color:var(--green-light)}
    .home-stat .lbl{font-size:0.74rem;color:var(--muted);margin-top:3px}
    /* DASHBOARD */
    .dash-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:16px;margin-bottom:20px}
    .metric-card{background:var(--card-bg);border:1px solid var(--glass-border);backdrop-filter:blur(12px);border-radius:var(--radius);padding:20px;display:flex;flex-direction:column;gap:7px;box-shadow:var(--shadow);position:relative;overflow:hidden}
    .metric-card::before{content:'';position:absolute;top:-30px;right:-30px;width:90px;height:90px;border-radius:50%;background:rgba(82,201,126,0.07)}
    .metric-icon{font-size:1.5rem}
    .metric-val{font-size:1.9rem;font-weight:800;color:var(--green-light)}
    .metric-lbl{font-size:0.8rem;color:var(--muted)}
    .metric-trend{font-size:0.75rem;color:#52c97e;margin-top:2px}
    .dash-charts{display:grid;grid-template-columns:1fr 1fr;gap:16px}
    .chart-card{background:var(--card-bg);border:1px solid var(--glass-border);backdrop-filter:blur(12px);border-radius:var(--radius);padding:20px;box-shadow:var(--shadow)}
    .chart-title{font-size:0.88rem;font-weight:700;color:var(--text);margin-bottom:14px}
    .bar-chart{display:flex;gap:8px;align-items:flex-end;height:100px}
    .bar-wrap{display:flex;flex-direction:column;align-items:center;gap:5px;flex:1}
    .bar{width:100%;border-radius:6px 6px 0 0;background:linear-gradient(180deg,var(--green-light),var(--green-dark));transition:height 0.6s ease;min-height:6px}
    .bar-lbl{font-size:0.64rem;color:var(--muted)}
    .donut-wrap{display:flex;align-items:center;gap:18px}
    .donut-legend{display:flex;flex-direction:column;gap:7px}
    .legend-item{display:flex;align-items:center;gap:8px;font-size:0.77rem;color:var(--muted)}
    .legend-dot{width:9px;height:9px;border-radius:50%;flex-shrink:0}
    /* SCAN */
    .scan-layout{display:grid;grid-template-columns:1fr 1fr;gap:20px;height:100%}
    .scan-camera-box{background:var(--card-bg);border:1px solid var(--glass-border);border-radius:var(--radius);overflow:hidden;position:relative;min-height:320px;display:flex;flex-direction:column;align-items:center;justify-content:center;box-shadow:var(--shadow)}
    #videoPreview{width:100%;height:100%;object-fit:cover;display:none;border-radius:var(--radius)}
    .scan-placeholder{display:flex;flex-direction:column;align-items:center;gap:10px;color:var(--muted)}
    .scan-placeholder i{font-size:3rem;color:var(--green-dark)}
    .scan-overlay{position:absolute;inset:0;border-radius:var(--radius);display:none;align-items:center;justify-content:center;background:rgba(0,0,0,0.3)}
    .scan-crosshair{width:150px;height:150px;border:3px solid var(--green-light);border-radius:14px;animation:pulseBorder 1.5s ease-in-out infinite}
    @keyframes pulseBorder{0%,100%{box-shadow:0 0 0 0 rgba(82,201,126,0.5)}50%{box-shadow:0 0 0 14px rgba(82,201,126,0)}}
    .scan-controls{display:flex;flex-direction:column;gap:14px}
    .detect-result{background:rgba(39,174,96,0.1);border:1px solid rgba(82,201,126,0.3);border-radius:12px;padding:16px;display:none}
    .detect-result.show{display:block;animation:fadeIn .4s ease}
    .detect-tag{font-size:0.95rem;font-weight:700;color:var(--green-light);margin-bottom:8px}
    .detect-list{display:flex;flex-direction:column;gap:5px}
    .detect-row{display:flex;justify-content:space-between;font-size:0.8rem;color:var(--muted)}
    .detect-row span:last-child{color:var(--text);font-weight:600}
    .scan-history{display:flex;flex-direction:column;gap:8px}
    .hist-item{display:flex;align-items:center;gap:10px;background:rgba(255,255,255,0.04);border:1px solid var(--glass-border);border-radius:10px;padding:9px 12px;font-size:0.8rem}
    .hist-item i{color:var(--green-light);font-size:0.9rem}
    .hist-info{flex:1}
    .hist-info .name{font-weight:600;color:var(--text)}
    .hist-info .time{color:var(--muted);font-size:0.72rem}
    .hist-pts{color:var(--accent);font-weight:700;font-size:0.8rem}
    /* REWARDS */
    .rewards-top{display:grid;grid-template-columns:320px 1fr;gap:20px;margin-bottom:20px}
    .wallet-card{background:linear-gradient(135deg,#1a5c38 0%,#0d3d22 60%,#0b2e1a 100%);border:1px solid rgba(82,201,126,0.25);border-radius:20px;padding:26px;box-shadow:0 12px 40px rgba(0,0,0,0.4);position:relative;overflow:hidden}
    .wallet-card::before{content:'';position:absolute;top:-40px;right:-40px;width:180px;height:180px;border-radius:50%;background:rgba(82,201,126,0.07)}
    .wallet-label{font-size:0.75rem;color:var(--muted);text-transform:uppercase;letter-spacing:.8px}
    .wallet-amount{font-size:2.6rem;font-weight:900;color:var(--accent);margin:5px 0 2px}
    .wallet-sub{font-size:0.8rem;color:var(--muted);margin-bottom:18px}
    .wallet-row{display:flex;justify-content:space-between}
    .wallet-info{font-size:0.78rem;color:var(--muted)}
    .wallet-info strong{color:var(--text)}
    .offer-cards{display:flex;flex-direction:column;gap:10px}
    .offer-item{display:flex;align-items:center;gap:12px;background:var(--card-bg);border:1px solid var(--glass-border);border-radius:12px;padding:12px 16px;transition:var(--transition)}
    .offer-item:hover{border-color:rgba(82,201,126,0.35);transform:translateX(3px)}
    .offer-icon{font-size:1.6rem;width:38px;text-align:center}
    .offer-info{flex:1}
    .offer-info .title{font-weight:700;font-size:0.86rem;color:var(--text)}
    .offer-info .desc{font-size:0.74rem;color:var(--muted);margin-top:2px}
    .offer-cost{font-weight:800;color:var(--accent);font-size:0.88rem}
    .redeem-btn{padding:6px 12px;border-radius:8px;border:none;background:rgba(240,192,64,0.18);color:var(--accent);font-size:0.76rem;font-weight:700;cursor:pointer;transition:var(--transition)}
    .redeem-btn:hover{background:rgba(240,192,64,0.3)}
    .rh-title{font-size:0.88rem;font-weight:700;color:var(--text);margin-bottom:12px}
    .rh-list{display:flex;flex-direction:column;gap:7px}
    .rh-item{display:flex;align-items:center;justify-content:space-between;background:rgba(255,255,255,0.04);border:1px solid var(--glass-border);border-radius:10px;padding:9px 14px;font-size:0.8rem}
    .rh-item .rh-desc{color:var(--muted)}
    .rh-item .rh-pts{font-weight:700;color:var(--green-light)}
    .rh-item .rh-pts.minus{color:#ff8080}
    /* MAP */
    .map-layout{display:grid;grid-template-columns:270px 1fr;gap:20px;height:calc(100vh - 200px)}
    .map-sidebar{display:flex;flex-direction:column;gap:12px;overflow-y:auto}
    .map-filter-label{font-size:0.75rem;color:var(--muted);font-weight:600;text-transform:uppercase;letter-spacing:.5px;margin-bottom:4px}
    .filter-chips{display:flex;flex-wrap:wrap;gap:7px}
    .chip{padding:5px 11px;border-radius:20px;font-size:0.75rem;font-weight:600;border:1px solid var(--glass-border);background:rgba(255,255,255,0.05);color:var(--muted);cursor:pointer;transition:var(--transition)}
    .chip.active,.chip:hover{background:rgba(39,174,96,0.2);border-color:var(--green-light);color:var(--green-light)}
    .nearby-list{display:flex;flex-direction:column;gap:7px}
    .nearby-item{background:var(--card-bg);border:1px solid var(--glass-border);border-radius:10px;padding:11px 13px;cursor:pointer;transition:var(--transition)}
    .nearby-item:hover{border-color:rgba(82,201,126,0.35)}
    .nearby-item .ni-name{font-size:0.82rem;font-weight:700;color:var(--text)}
    .nearby-item .ni-dist{font-size:0.72rem;color:var(--muted);margin-top:2px}
    .nearby-item .ni-status{font-size:0.7rem;font-weight:700;margin-top:4px}
    .map-placeholder{background:var(--card-bg);border:1px solid var(--glass-border);border-radius:var(--radius);overflow:hidden;position:relative;box-shadow:var(--shadow)}
    .map-grid-bg{width:100%;height:100%;background:repeating-linear-gradient(0deg,rgba(255,255,255,0.02) 0,rgba(255,255,255,0.02) 1px,transparent 1px,transparent 40px),repeating-linear-gradient(90deg,rgba(255,255,255,0.02) 0,rgba(255,255,255,0.02) 1px,transparent 1px,transparent 40px);position:absolute;inset:0}
    .road-h{position:absolute;height:4px;left:0;right:0;background:rgba(255,255,255,0.07);border-radius:2px}
    .road-v{position:absolute;width:4px;top:0;bottom:0;background:rgba(255,255,255,0.07);border-radius:2px}
    .map-pin{position:absolute;cursor:pointer;transform:translate(-50%,-100%);filter:drop-shadow(0 4px 8px rgba(0,0,0,0.5));transition:var(--transition);font-size:1.6rem;line-height:1}
    .map-pin:hover{transform:translate(-50%,-110%) scale(1.2)}
    .map-overlay-label{position:absolute;left:14px;top:14px;background:rgba(0,0,0,0.55);backdrop-filter:blur(8px);border:1px solid var(--glass-border);border-radius:10px;padding:7px 13px;font-size:0.8rem;color:var(--text)}
    .map-legend{position:absolute;right:14px;bottom:14px;background:rgba(0,0,0,0.55);backdrop-filter:blur(8px);border:1px solid var(--glass-border);border-radius:10px;padding:11px 15px;font-size:0.75rem;color:var(--muted);display:flex;flex-direction:column;gap:5px}
    /* SMART DUSTBIN */
    .dustbin-layout{display:grid;grid-template-columns:1fr 1fr;gap:20px}
    .dustbin-visual{display:flex;flex-direction:column;align-items:center;gap:16px}
    .dustbin-handle-top{width:46px;height:11px;background:var(--green-mid);border-radius:6px 6px 0 0;margin:0 auto}
    .dustbin-lid{width:150px;height:18px;background:linear-gradient(180deg,#27ae60,#1a7a40);border-radius:5px 5px 0 0;border:2px solid rgba(82,201,126,0.3);margin:0 auto}
    .dustbin-body{width:130px;height:170px;margin:0 auto;background:linear-gradient(180deg,#1e4a2c,#0d2e18);border:2px solid var(--green-dark);border-radius:0 0 18px 18px;position:relative;overflow:hidden}
    .dustbin-fill{position:absolute;bottom:0;left:0;right:0;background:linear-gradient(180deg,var(--green-light),var(--green-dark));border-radius:0 0 16px 16px;transition:height 0.8s ease;opacity:0.75}
    .dustbin-level{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;font-size:1.7rem;font-weight:900;color:#fff;text-shadow:0 2px 8px rgba(0,0,0,0.5);z-index:2}
    .bin-stats{display:flex;gap:14px;flex-wrap:wrap;justify-content:center}
    .bin-stat{background:var(--card-bg);border:1px solid var(--glass-border);border-radius:12px;padding:11px 16px;text-align:center}
    .bin-stat .val{font-size:1.3rem;font-weight:800;color:var(--green-light)}
    .bin-stat .lbl{font-size:0.72rem;color:var(--muted)}
    .deposit-btn{width:100%;padding:13px;border:none;border-radius:12px;background:linear-gradient(135deg,var(--green-mid),var(--accent2));color:#fff;font-size:0.95rem;font-weight:700;cursor:pointer;transition:var(--transition);box-shadow:0 4px 18px rgba(39,174,96,0.3)}
    .deposit-btn:hover{transform:translateY(-2px);box-shadow:0 8px 28px rgba(39,174,96,0.45)}
    .deposit-btn:active{transform:scale(0.97)}
    .deposit-log{display:flex;flex-direction:column;gap:7px;max-height:180px;overflow-y:auto}
    .log-item{display:flex;align-items:center;justify-content:space-between;background:rgba(255,255,255,0.04);border-radius:8px;padding:7px 11px;font-size:0.78rem;animation:fadeIn .3s ease}
    .log-item .log-time{color:var(--muted)}
    .log-item .log-pts{color:var(--accent);font-weight:700}
    .bin-alert{padding:11px 15px;border-radius:10px;font-size:0.82rem;font-weight:600;text-align:center}
    .bin-alert.ok{background:rgba(39,174,96,0.12);color:var(--green-light);border:1px solid rgba(82,201,126,0.3)}
    .bin-alert.warn{background:rgba(240,192,64,0.12);color:var(--accent);border:1px solid rgba(240,192,64,0.3)}
    .bin-alert.full{background:rgba(255,100,100,0.12);color:#ff8080;border:1px solid rgba(255,100,100,0.3)}
    /* LEADERBOARD */
    .lb-layout{display:grid;grid-template-columns:1fr 320px;gap:20px}
    .lb-top3{display:flex;align-items:flex-end;justify-content:center;gap:14px;margin-bottom:20px}
    .lb-podium{display:flex;flex-direction:column;align-items:center;gap:7px}
    .lb-podium .avatar{border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:800;color:#fff;border:3px solid transparent}
    .lb-podium.rank1 .avatar{width:66px;height:66px;font-size:1.1rem;background:linear-gradient(135deg,#f0c040,#e0a020);border-color:#f0c040}
    .lb-podium.rank2 .avatar{width:52px;height:52px;background:linear-gradient(135deg,#aaa,#777);border-color:#aaa}
    .lb-podium.rank3 .avatar{width:48px;height:48px;background:linear-gradient(135deg,#cd7f32,#a05a20);border-color:#cd7f32}
    .lb-podium .pname{font-size:0.8rem;font-weight:700;color:var(--text)}
    .lb-podium .ppts{font-size:0.75rem;color:var(--muted)}
    .lb-podium .rank-badge{font-size:0.72rem;font-weight:800;padding:3px 8px;border-radius:20px}
    .rank1 .rank-badge{background:rgba(240,192,64,0.2);color:var(--accent)}
    .rank2 .rank-badge{background:rgba(170,170,170,0.2);color:#aaa}
    .rank3 .rank-badge{background:rgba(205,127,50,0.2);color:#cd7f32}
    .lb-stand{width:100%;border-radius:5px 5px 0 0;background:rgba(255,255,255,0.08);margin-top:4px}
    .rank1 .lb-stand{height:65px}.rank2 .lb-stand{height:46px}.rank3 .lb-stand{height:32px}
    .lb-table{display:flex;flex-direction:column;gap:7px}
    .lb-row{display:grid;grid-template-columns:38px 1fr auto auto;align-items:center;gap:12px;background:var(--card-bg);border:1px solid var(--glass-border);border-radius:12px;padding:11px 14px;transition:var(--transition)}
    .lb-row:hover{border-color:rgba(82,201,126,0.3)}
    .lb-row.you{border-color:rgba(82,201,126,0.5);background:rgba(39,174,96,0.1)}
    .lb-rank-num{font-size:0.88rem;font-weight:800;color:var(--muted);text-align:center}
    .lb-user{display:flex;align-items:center;gap:9px}
    .lb-user .av{width:32px;height:32px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:0.75rem;font-weight:800;color:#fff;flex-shrink:0}
    .lb-user .uname{font-size:0.84rem;font-weight:600;color:var(--text)}
    .lb-user .ulvl{font-size:0.7rem;color:var(--muted)}
    .lb-pts-col{font-size:0.88rem;font-weight:800;color:var(--accent);text-align:right}
    .lb-change{font-size:0.72rem;font-weight:700}
    .lb-change.up{color:var(--green-light)}.lb-change.down{color:#ff8080}.lb-change.same{color:var(--muted)}
    .lb-your-rank{background:var(--card-bg);border:1px solid rgba(82,201,126,0.3);border-radius:var(--radius);padding:22px;text-align:center}
    .lyr-title{font-size:0.77rem;color:var(--muted);text-transform:uppercase;letter-spacing:.5px;margin-bottom:8px}
    .lyr-rank{font-size:2.8rem;font-weight:900;color:var(--green-light)}
    .lyr-of{font-size:0.82rem;color:var(--muted);margin-bottom:12px}
    .lyr-prog{background:rgba(255,255,255,0.08);border-radius:20px;height:7px;margin:10px 0;overflow:hidden}
    .lyr-bar{height:100%;background:linear-gradient(90deg,var(--green-mid),var(--green-light));border-radius:20px}
    /* PROFILE */
    .profile-layout{display:grid;grid-template-columns:280px 1fr;gap:20px}
    .profile-card{background:var(--card-bg);border:1px solid var(--glass-border);border-radius:var(--radius);padding:26px;text-align:center;box-shadow:var(--shadow)}
    .profile-avatar{width:84px;height:84px;border-radius:50%;background:linear-gradient(135deg,var(--green-mid),var(--accent2));display:flex;align-items:center;justify-content:center;font-size:2rem;font-weight:800;color:#fff;margin:0 auto 12px;border:3px solid rgba(82,201,126,0.4)}
    .profile-name{font-size:1.15rem;font-weight:800;color:var(--text);margin-bottom:4px}
    .profile-stats{display:flex;justify-content:space-around;margin:14px 0}
    .ps-item .val{font-size:1.3rem;font-weight:800;color:var(--green-light)}
    .ps-item .lbl{font-size:0.7rem;color:var(--muted)}
    .profile-info{display:flex;flex-direction:column;gap:7px;margin-top:10px}
    .pi-row{display:flex;align-items:center;gap:9px;font-size:0.8rem;color:var(--muted)}
    .pi-row i{color:var(--green-light);width:14px}
    .achievements{display:grid;grid-template-columns:1fr 1fr;gap:12px}
    .ach-card{background:var(--card-bg);border:1px solid var(--glass-border);border-radius:14px;padding:16px;display:flex;align-items:center;gap:12px;transition:var(--transition)}
    .ach-card:hover{border-color:rgba(82,201,126,0.3);transform:translateY(-2px)}
    .ach-card.locked{opacity:0.42}
    .ach-icon{font-size:1.8rem;flex-shrink:0}
    .ach-info .title{font-size:0.84rem;font-weight:700;color:var(--text)}
    .ach-info .desc{font-size:0.72rem;color:var(--muted);margin-top:2px}
    .ach-info .prog{margin-top:5px;background:rgba(255,255,255,0.08);border-radius:20px;height:4px;overflow:hidden}
    .ach-info .prog span{display:block;height:100%;background:var(--green-light);border-radius:20px}
    /* CONTACT */
    .contact-layout{display:grid;grid-template-columns:290px 1fr;gap:20px;height:calc(100vh - 175px)}
    .contact-info{display:flex;flex-direction:column;gap:13px}
    .contact-item{display:flex;align-items:center;gap:13px;background:var(--card-bg);border:1px solid var(--glass-border);border-radius:14px;padding:14px 16px}
    .contact-item .ci-icon{width:40px;height:40px;border-radius:10px;background:rgba(39,174,96,0.15);border:1px solid rgba(82,201,126,0.3);display:flex;align-items:center;justify-content:center;font-size:1rem;color:var(--green-light);flex-shrink:0}
    .contact-item .ci-label{font-size:0.72rem;color:var(--muted);text-transform:uppercase;letter-spacing:.5px}
    .contact-item .ci-value{font-size:0.86rem;font-weight:600;color:var(--text);margin-top:2px}
    .form-section{background:var(--card-bg);border:1px solid var(--glass-border);border-radius:var(--radius);padding:22px;display:flex;flex-direction:column}
    .form-section h3{font-size:0.96rem;font-weight:700;color:var(--text);margin-bottom:4px}
    .form-section .form-note{font-size:0.78rem;color:var(--muted);margin-bottom:12px}
    .gform-iframe{flex:1;width:100%;border:none;border-radius:10px;background:rgba(255,255,255,0.02);min-height:460px}
    /* TOAST */
    #toast{position:fixed;bottom:26px;right:26px;z-index:9999;padding:11px 18px;border-radius:12px;background:rgba(30,70,45,0.95);border:1px solid var(--green-light);color:var(--text);font-size:0.85rem;font-weight:600;backdrop-filter:blur(12px);box-shadow:var(--shadow);transform:translateY(80px);opacity:0;transition:all 0.4s cubic-bezier(.4,0,.2,1);display:flex;align-items:center;gap:9px}
    #toast.show{transform:translateY(0);opacity:1}
    #toast i{color:var(--green-light)}
  </style>
</head>
<body>

<!-- Background Blobs -->
<div class="bg-blobs">
  <div class="blob blob1"></div>
  <div class="blob blob2"></div>
  <div class="blob blob3"></div>
</div>

<!-- ============================================================ AUTH SCREEN ============================================================ -->
<div id="authScreen">
  <div class="auth-box">
    <div class="auth-logo">
      <i class="fas fa-leaf logo-icon"></i>
      <h1>EcoTrack</h1>
      <p>Smart Plastic Waste Management System</p>
    </div>
    <div class="auth-tabs">
      <button class="auth-tab active" onclick="switchTab('login',this)">Login</button>
      <button class="auth-tab" onclick="switchTab('signup',this)">Sign Up</button>
    </div>
    <!-- Login Form -->
    <div id="loginForm" class="auth-form">
      <div class="form-group"><label>Email</label><input type="email" id="loginEmail" placeholder="you@example.com"/></div>
      <div class="form-group"><label>Password</label><input type="password" id="loginPass" placeholder="Enter password" onkeydown="if(event.key==='Enter')handleLogin()"/></div>
      <p class="auth-error" id="loginError"></p>
      <button class="auth-btn" onclick="handleLogin()"><i class="fas fa-sign-in-alt"></i> Login</button>
    </div>
    <!-- Signup Form -->
    <div id="signupForm" class="auth-form" style="display:none">
      <div class="form-group"><label>Full Name</label><input type="text" id="signupName" placeholder="Your full name"/></div>
      <div class="form-group"><label>Email</label><input type="email" id="signupEmail" placeholder="you@example.com"/></div>
      <div class="form-group"><label>Password</label><input type="password" id="signupPass" placeholder="Min 6 characters" onkeydown="if(event.key==='Enter')handleSignup()"/></div>
      <p class="auth-error" id="signupError"></p>
      <button class="auth-btn" onclick="handleSignup()"><i class="fas fa-user-plus"></i> Create Account</button>
    </div>
    <p class="auth-quote">"The Earth does not belong to us, we belong to the Earth."</p>
  </div>
</div>

<!-- ============================================================ MAIN APP ============================================================ -->
<div id="app">
  <!-- NAVBAR -->
  <nav>
    <div class="nav-brand" onclick="showSection('home')">
      <i class="fas fa-leaf leaf"></i>
      <span>EcoTrack</span>
    </div>
    <div class="nav-links">
      <button class="nav-btn active" id="nav-home"        onclick="showSection('home')"><i class="fas fa-home"></i> Home</button>
      <button class="nav-btn"        id="nav-dashboard"   onclick="showSection('dashboard')"><i class="fas fa-chart-bar"></i> Dashboard</button>
      <button class="nav-btn"        id="nav-scan"        onclick="showSection('scan')"><i class="fas fa-camera"></i> Scan Plastic</button>
      <button class="nav-btn"        id="nav-rewards"     onclick="showSection('rewards')"><i class="fas fa-gift"></i> Rewards</button>
      <button class="nav-btn"        id="nav-map"         onclick="showSection('map')"><i class="fas fa-map-marked-alt"></i> Map</button>
      <button class="nav-btn"        id="nav-smartdusbin" onclick="showSection('smartdusbin')"><i class="fas fa-trash-alt"></i> Smart Dustbin</button>
      <button class="nav-btn"        id="nav-leaderboard" onclick="showSection('leaderboard')"><i class="fas fa-trophy"></i> Leaderboard</button>
      <button class="nav-btn"        id="nav-profile"     onclick="showSection('profile')"><i class="fas fa-user"></i> Profile</button>
      <button class="nav-btn"        id="nav-contact"     onclick="showSection('contact')"><i class="fas fa-envelope"></i> Contact</button>
    </div>
    <div class="nav-right">
      <div class="nav-credits"><i class="fas fa-coins"></i><span id="navCredits">240</span> Credits</div>
      <div class="nav-user-avatar" id="navAvatar">A</div>
      <button class="logout-btn" onclick="handleLogout()"><i class="fas fa-sign-out-alt"></i> Logout</button>
    </div>
  </nav>

  <!-- CONTENT -->
  <div id="content">

    <!-- ===== 1. HOME ===== -->
    <div class="section active" id="home" style="display:flex;flex-direction:column;justify-content:center;align-items:center;text-align:center;min-height:calc(100vh - 62px)">
      <div class="eco-quote" style="max-width:600px">🌿 <span>Every plastic bottle you recycle saves enough energy to power a light bulb for 6 hours.</span> Keep going — the planet is counting on you!</div>
      <div class="home-hero-icon">♻️</div>
      <h1 class="home-title">EcoTrack</h1>
      <p class="home-sub">A smart, gamified platform to track, scan, and recycle plastic waste — earn <strong style="color:var(--accent)">Plastic Credits</strong> and make our campus greener, one bottle at a time.</p>
      <div class="home-btns">
        <button class="btn-primary" onclick="showSection('scan')"><i class="fas fa-camera"></i> Scan Plastic Now</button>
        <button class="btn-outline" onclick="showSection('dashboard')"><i class="fas fa-chart-bar"></i> View Dashboard</button>
      </div>
      <div class="home-stats">
        <div class="home-stat"><div class="val">1,284</div><div class="lbl">Total Scans Today</div></div>
        <div class="home-stat"><div class="val">62 kg</div><div class="lbl">Plastic Collected</div></div>
        <div class="home-stat"><div class="val">340</div><div class="lbl">Active Users</div></div>
        <div class="home-stat"><div class="val">18</div><div class="lbl">Smart Dustbins</div></div>
      </div>
    </div>

    <!-- ===== 2. DASHBOARD ===== -->
    <div class="section" id="dashboard">
      <h2 class="section-title">Your Dashboard</h2>
      <p class="section-sub">Track your eco impact in real time</p>
      <div class="dash-grid">
        <div class="metric-card"><div class="metric-icon">🌿</div><div class="metric-val" id="dashScore">78</div><div class="metric-lbl">Eco Score</div><div class="metric-trend">↑ +5 this week</div><div class="progress-bar" style="margin-top:6px"><div class="progress-fill" style="width:78%"></div></div></div>
        <div class="metric-card"><div class="metric-icon">🪙</div><div class="metric-val" id="dashCredits">240</div><div class="metric-lbl">Plastic Credits</div><div class="metric-trend">↑ +30 today</div></div>
        <div class="metric-card"><div class="metric-icon">👣</div><div class="metric-val">2.1 kg</div><div class="metric-lbl">CO₂ Footprint Saved</div><div class="metric-trend">↓ Reduced 12%</div></div>
        <div class="metric-card"><div class="metric-icon">🔢</div><div class="metric-val" id="dashScanCount">23</div><div class="metric-lbl">Total Scans</div><div class="metric-trend">↑ 3 today</div></div>
        <div class="metric-card"><div class="metric-icon">🏆</div><div class="metric-val">#4</div><div class="metric-lbl">Leaderboard Rank</div><div class="metric-trend">↑ Up 2 spots</div></div>
        <div class="metric-card"><div class="metric-icon">🎯</div><div class="metric-val">Level 3</div><div class="metric-lbl">Eco Level</div><div class="metric-trend">450 XP to next level</div></div>
      </div>
      <div class="dash-charts">
        <div class="chart-card"><div class="chart-title">📊 Weekly Plastic Collected (kg)</div><div class="bar-chart" id="barChart"></div></div>
        <div class="chart-card">
          <div class="chart-title">🥧 Plastic Types Scanned</div>
          <div class="donut-wrap">
            <svg width="110" height="110" viewBox="0 0 120 120">
              <circle cx="60" cy="60" r="45" fill="none" stroke="rgba(255,255,255,0.06)" stroke-width="18"/>
              <circle cx="60" cy="60" r="45" fill="none" stroke="#27ae60" stroke-width="18" stroke-dasharray="113 170" stroke-dashoffset="0" transform="rotate(-90 60 60)"/>
              <circle cx="60" cy="60" r="45" fill="none" stroke="#3ecfcf" stroke-width="18" stroke-dasharray="68 215" stroke-dashoffset="-113" transform="rotate(-90 60 60)"/>
              <circle cx="60" cy="60" r="45" fill="none" stroke="#f0c040" stroke-width="18" stroke-dasharray="39 244" stroke-dashoffset="-181" transform="rotate(-90 60 60)"/>
              <circle cx="60" cy="60" r="45" fill="none" stroke="#ff8080" stroke-width="18" stroke-dasharray="30 253" stroke-dashoffset="-220" transform="rotate(-90 60 60)"/>
              <text x="60" y="65" text-anchor="middle" fill="#e8f5ee" font-size="11" font-weight="700">23 items</text>
            </svg>
            <div class="donut-legend">
              <div class="legend-item"><div class="legend-dot" style="background:#27ae60"></div>PET Bottles – 50%</div>
              <div class="legend-item"><div class="legend-dot" style="background:#3ecfcf"></div>HDPE Caps – 30%</div>
              <div class="legend-item"><div class="legend-dot" style="background:#f0c040"></div>LDPE Bags – 17%</div>
              <div class="legend-item"><div class="legend-dot" style="background:#ff8080"></div>Other – 13%</div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- ===== 3. SCAN ===== -->
    <div class="section" id="scan">
      <h2 class="section-title">Scan Plastic</h2>
      <p class="section-sub">Point camera at plastic — AI will detect it automatically (prototype simulation)</p>
      <div class="scan-layout">
        <!-- Camera Box -->
        <div class="scan-camera-box">
          <video id="videoPreview" autoplay playsinline></video>
          <div class="scan-placeholder" id="scanPlaceholder">
            <i class="fas fa-camera"></i>
            <p style="font-weight:600">Camera Not Active</p>
            <p style="font-size:0.75rem">Click "Start Camera" to begin</p>
          </div>
          <div class="scan-overlay" id="scanOverlay">
            <div class="scan-crosshair"></div>
          </div>
        </div>
        <!-- Controls + Results -->
        <div class="scan-controls">
          <div class="card">
            <div class="flex-between" style="margin-bottom:14px">
              <div><div style="font-size:0.84rem;font-weight:700;color:var(--text)">Camera Controls</div><div style="font-size:0.75rem;color:var(--muted)">Allow camera permission when prompted</div></div>
              <div id="camStatus" class="badge badge-green" style="display:none">● LIVE</div>
            </div>
            <div style="display:flex;gap:9px">
              <button class="btn-primary" id="startCamBtn" onclick="startCamera()" style="flex:1;padding:10px;font-size:0.85rem"><i class="fas fa-video"></i> Start Camera</button>
              <button class="btn-outline"  id="stopCamBtn"  onclick="stopCamera()"  style="flex:1;padding:10px;font-size:0.85rem;display:none"><i class="fas fa-stop"></i> Stop Camera</button>
            </div>
          </div>
          <div class="card">
            <div style="font-size:0.84rem;font-weight:700;color:var(--text);margin-bottom:10px"><i class="fas fa-robot" style="color:var(--green-light)"></i> AI Detection (Prototype)</div>
            <button class="btn-primary" onclick="simulateDetect()" style="width:100%;padding:10px;font-size:0.85rem;margin-bottom:12px"><i class="fas fa-search"></i> Detect Plastic</button>
            <div class="detect-result" id="detectResult">
              <div class="detect-tag">✅ Detected: <span id="detectedType">Plastic Bottle (PET)</span></div>
              <div class="detect-list">
                <div class="detect-row"><span>AI Confidence</span><span id="confidence">94.3%</span></div>
                <div class="detect-row"><span>Recyclable</span><span style="color:#52c97e">Yes ✓</span></div>
                <div class="detect-row"><span>Credits Earned</span><span style="color:var(--accent)" id="earnedPts">+15</span></div>
                <div class="detect-row"><span>Eco Score Boost</span><span style="color:var(--green-light)">+3 pts</span></div>
              </div>
            </div>
          </div>
          <div class="card">
            <div style="font-size:0.84rem;font-weight:700;color:var(--text);margin-bottom:11px">Recent Scans</div>
            <div class="scan-history" id="scanHistory">
              <div class="hist-item"><i class="fas fa-recycle"></i><div class="hist-info"><div class="name">PET Bottle</div><div class="time">2 min ago</div></div><div class="hist-pts">+15 pts</div></div>
              <div class="hist-item"><i class="fas fa-recycle"></i><div class="hist-info"><div class="name">HDPE Cap</div><div class="time">18 min ago</div></div><div class="hist-pts">+8 pts</div></div>
              <div class="hist-item"><i class="fas fa-recycle"></i><div class="hist-info"><div class="name">Plastic Bag (LDPE)</div><div class="time">1 hr ago</div></div><div class="hist-pts">+10 pts</div></div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- ===== 4. REWARDS ===== -->
    <div class="section" id="rewards">
      <h2 class="section-title">Rewards & Wallet</h2>
      <p class="section-sub">Spend your Plastic Credits on real campus rewards</p>
      <div class="rewards-top">
        <div class="wallet-card">
          <div class="wallet-label">Plastic Credit Balance</div>
          <div class="wallet-amount" id="walletAmount">240</div>
          <div class="wallet-sub">≈ ₹24.00 equivalent value</div>
          <div class="wallet-row">
            <div class="wallet-info">Earned<br><strong id="walletEarned">560 PC</strong></div>
            <div class="wallet-info">Spent<br><strong>320 PC</strong></div>
            <div class="wallet-info">Status<br><strong style="color:var(--green-light)">Eco Hero</strong></div>
          </div>
        </div>
        <div class="card" style="padding:18px">
          <div style="font-size:0.88rem;font-weight:700;color:var(--text);margin-bottom:12px">🎁 Available Rewards</div>
          <div class="offer-cards">
            <div class="offer-item"><div class="offer-icon">☕</div><div class="offer-info"><div class="title">Free Canteen Coffee</div><div class="desc">Redeemable at VGU Canteen</div></div><div><div class="offer-cost">50 PC</div><button class="redeem-btn" onclick="redeemReward(50,'Free Coffee')">Redeem</button></div></div>
            <div class="offer-item"><div class="offer-icon">📚</div><div class="offer-info"><div class="title">Library Extra 1-Day Pass</div><div class="desc">Extended borrowing access</div></div><div><div class="offer-cost">80 PC</div><button class="redeem-btn" onclick="redeemReward(80,'Library Pass')">Redeem</button></div></div>
            <div class="offer-item"><div class="offer-icon">🎫</div><div class="offer-info"><div class="title">Campus Event Free Entry</div><div class="desc">Access to next eco event</div></div><div><div class="offer-cost">120 PC</div><button class="redeem-btn" onclick="redeemReward(120,'Event Entry')">Redeem</button></div></div>
            <div class="offer-item"><div class="offer-icon">🛍️</div><div class="offer-info"><div class="title">Eco Bag + Bottle Kit</div><div class="desc">Reusable campus kit</div></div><div><div class="offer-cost">200 PC</div><button class="redeem-btn" onclick="redeemReward(200,'Eco Kit')">Redeem</button></div></div>
          </div>
        </div>
      </div>
      <div class="card">
        <div class="rh-title">Transaction History</div>
        <div class="rh-list" id="rewardHistory">
          <div class="rh-item"><span class="rh-desc">PET Bottle Scanned</span><span>Today, 10:22 AM</span><span class="rh-pts">+15 PC</span></div>
          <div class="rh-item"><span class="rh-desc">Smart Dustbin Deposit</span><span>Today, 09:10 AM</span><span class="rh-pts">+20 PC</span></div>
          <div class="rh-item"><span class="rh-desc">Redeemed – Free Coffee</span><span>Yesterday</span><span class="rh-pts minus">-50 PC</span></div>
          <div class="rh-item"><span class="rh-desc">Weekly Eco Bonus</span><span>Monday</span><span class="rh-pts">+50 PC</span></div>
        </div>
      </div>
    </div>

    <!-- ===== 5. MAP ===== -->
    <div class="section" id="map">
      <h2 class="section-title">Nearby Recycling Points</h2>
      <p class="section-sub">Find smart dustbins and recycling centers on VGU Campus</p>
      <div class="map-layout">
        <div class="map-sidebar">
          <div class="card" style="padding:16px">
            <div class="map-filter-label">Filter by Type</div>
            <div class="filter-chips" style="margin-top:8px">
              <span class="chip active">All</span>
              <span class="chip">Smart Dustbins</span>
              <span class="chip">Recycling Centers</span>
              <span class="chip">Drop Zones</span>
            </div>
          </div>
          <div class="card" style="padding:16px">
            <div style="font-size:0.75rem;color:var(--muted);font-weight:600;text-transform:uppercase;letter-spacing:.5px;margin-bottom:9px">📍 Nearby Locations</div>
            <div class="nearby-list">
              <div class="nearby-item"><div class="ni-name">🗑️ Smart Bin – Block A</div><div class="ni-dist">120m away</div><div class="ni-status" style="color:var(--green-light)">● Available (45% full)</div></div>
              <div class="nearby-item"><div class="ni-name">🗑️ Smart Bin – Canteen</div><div class="ni-dist">200m away</div><div class="ni-status" style="color:var(--accent)">● Almost Full (82%)</div></div>
              <div class="nearby-item"><div class="ni-name">♻️ Recycling Hub – Main</div><div class="ni-dist">350m away</div><div class="ni-status" style="color:var(--green-light)">● Open Now</div></div>
              <div class="nearby-item"><div class="ni-name">🗑️ Smart Bin – Library</div><div class="ni-dist">80m away</div><div class="ni-status" style="color:var(--green-light)">● Available (22% full)</div></div>
              <div class="nearby-item"><div class="ni-name">🗑️ Smart Bin – Hostel B</div><div class="ni-dist">500m away</div><div class="ni-status" style="color:#ff8080">● Full – Collection Needed</div></div>
            </div>
          </div>
        </div>
        <!-- Map Placeholder Visual -->
        <div class="map-placeholder">
          <div class="map-grid-bg"></div>
          <div class="road-h" style="top:28%"></div><div class="road-h" style="top:53%"></div><div class="road-h" style="top:76%"></div>
          <div class="road-v" style="left:24%"></div><div class="road-v" style="left:58%"></div><div class="road-v" style="left:79%"></div>
          <div class="map-pin" style="left:25%;top:30%">🗑️</div>
          <div class="map-pin" style="left:60%;top:55%">🗑️</div>
          <div class="map-pin" style="left:41%;top:43%">♻️</div>
          <div class="map-pin" style="left:19%;top:58%">🗑️</div>
          <div class="map-pin" style="left:74%;top:28%">🗑️</div>
          <div class="map-pin" style="left:54%;top:76%">♻️</div>
          <div class="map-overlay-label">📍 VGU Campus, Jaipur, Rajasthan</div>
          <div class="map-legend">
            <div style="font-size:0.72rem;font-weight:700;color:var(--text);margin-bottom:3px">Legend</div>
            <div>🗑️ Smart Dustbin</div>
            <div>♻️ Recycling Center</div>
          </div>
        </div>
      </div>
    </div>

    <!-- ===== 6. SMART DUSTBIN ===== -->
    <div class="section" id="smartdusbin">
      <h2 class="section-title">Smart Dustbin</h2>
      <p class="section-sub">Deposit plastic items and earn Plastic Credits instantly</p>
      <div class="dustbin-layout">
        <!-- Visual Left -->
        <div class="card">
          <div class="dustbin-visual">
            <div>
              <div class="dustbin-handle-top"></div>
              <div class="dustbin-lid"></div>
              <div class="dustbin-body">
                <div class="dustbin-fill" id="binFill" style="height:45%"></div>
                <div class="dustbin-level" id="binLevelText">45%</div>
              </div>
            </div>
            <div class="bin-alert ok" id="binAlert">● Smart Bin – Block A (45% full)</div>
            <div class="bin-stats">
              <div class="bin-stat"><div class="val" id="binCount">12</div><div class="lbl">Items Today</div></div>
              <div class="bin-stat"><div class="val">1.2 kg</div><div class="lbl">Weight</div></div>
              <div class="bin-stat"><div class="val" id="binTemp">28°C</div><div class="lbl">Temp Sensor</div></div>
            </div>
          </div>
        </div>
        <!-- Right Column -->
        <div style="display:flex;flex-direction:column;gap:16px">
          <div class="card">
            <div style="font-size:0.9rem;font-weight:700;color:var(--text);margin-bottom:6px">💡 Plastic Credit Economy</div>
            <div style="font-size:0.8rem;color:var(--muted);margin-bottom:14px;line-height:1.65">Each plastic item deposited earns <strong style="color:var(--accent)">Plastic Credits (PC)</strong> — a campus token exchangeable for real rewards. Bigger items earn more credits. Help keep VGU clean and get rewarded! 🌿</div>
            <div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:9px;margin-bottom:14px">
              <div style="background:rgba(255,255,255,0.04);border-radius:10px;padding:10px;text-align:center"><div style="font-size:1rem">🍶</div><div style="font-size:0.74rem;color:var(--muted);margin-top:3px">Bottle</div><div style="font-size:0.84rem;font-weight:800;color:var(--accent)">+15 PC</div></div>
              <div style="background:rgba(255,255,255,0.04);border-radius:10px;padding:10px;text-align:center"><div style="font-size:1rem">🧴</div><div style="font-size:0.74rem;color:var(--muted);margin-top:3px">Container</div><div style="font-size:0.84rem;font-weight:800;color:var(--accent)">+20 PC</div></div>
              <div style="background:rgba(255,255,255,0.04);border-radius:10px;padding:10px;text-align:center"><div style="font-size:1rem">🛍️</div><div style="font-size:0.74rem;color:var(--muted);margin-top:3px">Bag</div><div style="font-size:0.84rem;font-weight:800;color:var(--accent)">+10 PC</div></div>
            </div>
            <button class="deposit-btn" onclick="simulateDeposit()"><i class="fas fa-plus-circle"></i> Simulate Deposit (+15 Credits)</button>
          </div>
          <div class="card">
            <div style="font-size:0.84rem;font-weight:700;color:var(--text);margin-bottom:11px">Deposit Log</div>
            <div class="deposit-log" id="depositLog">
              <div class="log-item"><span>PET Bottle deposited</span><span class="log-time">09:10 AM</span><span class="log-pts">+15 PC</span></div>
              <div class="log-item"><span>HDPE Container</span><span class="log-time">Yesterday</span><span class="log-pts">+20 PC</span></div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- ===== 7. LEADERBOARD ===== -->
    <div class="section" id="leaderboard">
      <h2 class="section-title">Leaderboard</h2>
      <p class="section-sub">Top eco-warriors at VGU Campus this month</p>
      <div class="lb-layout">
        <div>
          <!-- Podium Top 3 -->
          <div class="lb-top3">
            <div class="lb-podium rank2"><div class="avatar">SK</div><div class="pname">Sneha K.</div><div class="ppts">1840 PC</div><div class="rank-badge">🥈 #2</div><div class="lb-stand"></div></div>
            <div class="lb-podium rank1"><div class="avatar">RA</div><div class="pname">Rohan A.</div><div class="ppts">2350 PC</div><div class="rank-badge">🥇 #1</div><div class="lb-stand"></div></div>
            <div class="lb-podium rank3"><div class="avatar">PM</div><div class="pname">Priya M.</div><div class="ppts">1620 PC</div><div class="rank-badge">🥉 #3</div><div class="lb-stand"></div></div>
          </div>
          <!-- Full Table -->
          <div class="lb-table">
            <div class="lb-row you">
              <div class="lb-rank-num">#4</div>
              <div class="lb-user"><div class="av" style="background:linear-gradient(135deg,#27ae60,#3ecfcf)" id="lbYouAvatar">A</div><div><div class="uname" id="lbYouName">You</div><div class="ulvl">Eco Hero · Level 3</div></div></div>
              <div class="lb-pts-col" id="lbYouPts">240 PC</div>
              <div class="lb-change up">↑ 2</div>
            </div>
            <div class="lb-row"><div class="lb-rank-num">#5</div><div class="lb-user"><div class="av" style="background:linear-gradient(135deg,#8e44ad,#e74c3c)">VK</div><div><div class="uname">Vikram K.</div><div class="ulvl">Green Star · Level 2</div></div></div><div class="lb-pts-col">210 PC</div><div class="lb-change same">–</div></div>
            <div class="lb-row"><div class="lb-rank-num">#6</div><div class="lb-user"><div class="av" style="background:linear-gradient(135deg,#e67e22,#e74c3c)">NP</div><div><div class="uname">Nisha P.</div><div class="ulvl">Eco Starter · Level 1</div></div></div><div class="lb-pts-col">190 PC</div><div class="lb-change down">↓ 1</div></div>
            <div class="lb-row"><div class="lb-rank-num">#7</div><div class="lb-user"><div class="av" style="background:linear-gradient(135deg,#2980b9,#8e44ad)">AS</div><div><div class="uname">Arjun S.</div><div class="ulvl">Eco Starter · Level 1</div></div></div><div class="lb-pts-col">165 PC</div><div class="lb-change up">↑ 1</div></div>
          </div>
        </div>
        <!-- Your Rank Panel -->
        <div style="display:flex;flex-direction:column;gap:14px">
          <div class="lb-your-rank">
            <div class="lyr-title">Your Rank This Month</div>
            <div class="lyr-rank">#4</div>
            <div class="lyr-of">out of 340 participants</div>
            <div class="lyr-prog"><div class="lyr-bar" style="width:68%"></div></div>
            <div style="font-size:0.8rem;color:var(--muted)">Top 2% — you're in the <strong style="color:var(--green-light)">Elite Zone</strong>!</div>
            <div style="margin-top:16px;display:flex;flex-direction:column;gap:7px">
              <div class="flex-between" style="font-size:0.78rem"><span style="color:var(--muted)">Credits to reach #3</span><span style="color:var(--accent);font-weight:700">+1380 PC</span></div>
              <div class="flex-between" style="font-size:0.78rem"><span style="color:var(--muted)">Scans this month</span><span style="color:var(--text);font-weight:700">23</span></div>
              <div class="flex-between" style="font-size:0.78rem"><span style="color:var(--muted)">Best rank ever</span><span style="color:var(--green-light);font-weight:700">#2</span></div>
            </div>
          </div>
          <div class="eco-quote">🌱 <span>"Be the change you wish to see in the world."</span> — Gandhi</div>
        </div>
      </div>
    </div>

    <!-- ===== 8. PROFILE ===== -->
    <div class="section" id="profile">
      <h2 class="section-title">My Profile</h2>
      <p class="section-sub">Your eco journey at a glance</p>
      <div class="profile-layout">
        <div class="profile-card">
          <div class="profile-avatar" id="profileAvatar">A</div>
          <div class="profile-name" id="profileName">Alex Johnson</div>
          <div style="margin-bottom:12px"><span class="badge badge-green">Eco Hero · Level 3</span></div>
          <div class="progress-bar"><div class="progress-fill" style="width:68%"></div></div>
          <div style="display:flex;justify-content:space-between;font-size:0.7rem;color:var(--muted);margin-top:4px"><span>Level 3</span><span>68% to Level 4</span></div>
          <div class="profile-stats">
            <div class="ps-item"><div class="val" id="profCredits">240</div><div class="lbl">Credits</div></div>
            <div class="ps-item"><div class="val" id="profScans">23</div><div class="lbl">Scans</div></div>
            <div class="ps-item"><div class="val">#4</div><div class="lbl">Rank</div></div>
          </div>
          <div class="profile-info">
            <div class="pi-row"><i class="fas fa-envelope"></i><span id="profEmail">alex@vgu.ac.in</span></div>
            <div class="pi-row"><i class="fas fa-university"></i><span>VGU Jaipur</span></div>
            <div class="pi-row"><i class="fas fa-calendar"></i><span>Joined April 2025</span></div>
            <div class="pi-row"><i class="fas fa-leaf"></i><span>2.1 kg CO₂ saved</span></div>
          </div>
        </div>
        <div>
          <div style="font-size:0.9rem;font-weight:700;color:var(--text);margin-bottom:14px">🏅 Achievements</div>
          <div class="achievements">
            <div class="ach-card"><div class="ach-icon">🌱</div><div class="ach-info"><div class="title">First Step</div><div class="desc">Completed first scan</div><div class="prog"><span style="width:100%"></span></div></div></div>
            <div class="ach-card"><div class="ach-icon">🔟</div><div class="ach-info"><div class="title">10 Scans Done</div><div class="desc">Scanned 10 plastic items</div><div class="prog"><span style="width:100%"></span></div></div></div>
            <div class="ach-card"><div class="ach-icon">🏆</div><div class="ach-info"><div class="title">Eco Hero</div><div class="desc">Reached Level 3</div><div class="prog"><span style="width:100%"></span></div></div></div>
            <div class="ach-card"><div class="ach-icon">⭐</div><div class="ach-info"><div class="title">Top 5 Rank</div><div class="desc">Ranked in top 5</div><div class="prog"><span style="width:100%"></span></div></div></div>
            <div class="ach-card locked"><div class="ach-icon">💎</div><div class="ach-info"><div class="title">Diamond Recycler</div><div class="desc">500 items recycled</div><div class="prog"><span style="width:23%"></span></div></div></div>
            <div class="ach-card locked"><div class="ach-icon">🌍</div><div class="ach-info"><div class="title">Planet Saver</div><div class="desc">Save 10 kg CO₂</div><div class="prog"><span style="width:21%"></span></div></div></div>
            <div class="ach-card locked"><div class="ach-icon">🔥</div><div class="ach-info"><div class="title">30-Day Streak</div><div class="desc">Scan every day for 30 days</div><div class="prog"><span style="width:43%"></span></div></div></div>
            <div class="ach-card locked"><div class="ach-icon">👑</div><div class="ach-info"><div class="title">#1 Champion</div><div class="desc">Reach leaderboard #1</div><div class="prog"><span style="width:10%"></span></div></div></div>
          </div>
        </div>
      </div>
    </div>

    <!-- ===== 9. CONTACT ===== -->
    <div class="section" id="contact">
      <h2 class="section-title">Contact Us</h2>
      <p class="section-sub">Get in touch with the EcoTrack team at VGU Jaipur</p>
      <div class="contact-layout">
        <!-- Info Column -->
        <div class="contact-info">
          <div class="contact-item">
            <div class="ci-icon"><i class="fas fa-envelope"></i></div>
            <div><div class="ci-label">Email</div><div class="ci-value">24csa2bc151@vgu.ac.in</div></div>
          </div>
          <div class="contact-item">
            <div class="ci-icon"><i class="fas fa-phone"></i></div>
            <div><div class="ci-label">Phone</div><div class="ci-value">+91 7991187225</div></div>
          </div>
          <div class="contact-item">
            <div class="ci-icon"><i class="fas fa-map-marker-alt"></i></div>
            <div><div class="ci-label">Location</div><div class="ci-value">VGU Jaipur, Rajasthan</div></div>
          </div>
          <div class="card" style="padding:16px">
            <div style="font-size:0.84rem;font-weight:700;color:var(--text);margin-bottom:8px">About This Project</div>
            <div style="font-size:0.78rem;color:var(--muted);line-height:1.7"><strong style="color:var(--text)">EcoTrack</strong> is a college project developed at <strong style="color:var(--green-light)">VGU Jaipur</strong>. It demonstrates a smart plastic waste management system using IoT sensors, AI detection, and gamification to encourage recycling on campus.</div>
          </div>
          <div class="eco-quote">🌎 <span>"Small acts, when multiplied by millions of people, can transform the world."</span></div>
        </div>
        <!-- Google Form -->
        <div class="form-section">
          <h3>Send us a message</h3>
          <p class="form-note">Fill this form and your message will be sent directly to us</p>
          <iframe
            class="gform-iframe"
            src="https://docs.google.com/forms/d/e/1FAIpQLSeAURWmUEINTLQ0iS6N-PYtEWvKrRA0GNk3KDe1f9jNdWCFvw/viewform?embedded=true"
            title="EcoTrack Contact Form"
            loading="lazy">Loading form…</iframe>
        </div>
      </div>
    </div>

  </div><!-- /#content -->
</div><!-- /#app -->

<!-- Toast -->
<div id="toast"><i class="fas fa-check-circle"></i><span id="toastMsg">Success!</span></div>

<script>
/* ============================================================
   STATE
============================================================ */
const state={loggedIn:false,userName:'Alex Johnson',userEmail:'alex@vgu.ac.in',credits:240,scanCount:23,binLevel:45,binDeposits:0,cameraStream:null,detecting:false};
const PLASTICS=[{name:'Plastic Bottle (PET)',pts:15,conf:'94.3%'},{name:'HDPE Container',pts:20,conf:'91.7%'},{name:'Plastic Bag (LDPE)',pts:10,conf:'88.1%'},{name:'Styrofoam Cup (PS)',pts:12,conf:'86.5%'},{name:'PVC Pipe Piece',pts:18,conf:'89.9%'},{name:'Polypropylene Cap',pts:8,conf:'92.2%'}];

/* ============================================================
   NAVIGATION
============================================================ */
function showSection(id){
  document.querySelectorAll('.section').forEach(s=>s.classList.remove('active'));
  const t=document.getElementById(id);
  if(t)t.classList.add('active');
  document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));
  const nb=document.getElementById('nav-'+id);
  if(nb)nb.classList.add('active');
  if(id!=='scan'&&state.cameraStream)stopCamera();
}

/* ============================================================
   AUTH
============================================================ */
function switchTab(tab,el){
  document.querySelectorAll('.auth-tab').forEach(t=>t.classList.remove('active'));
  el.classList.add('active');
  document.getElementById('loginForm').style.display=tab==='login'?'flex':'none';
  document.getElementById('signupForm').style.display=tab==='signup'?'flex':'none';
  document.getElementById('loginError').textContent='';
  document.getElementById('signupError').textContent='';
}

function handleLogin(){
  const email=document.getElementById('loginEmail').value.trim();
  const pass=document.getElementById('loginPass').value.trim();
  const err=document.getElementById('loginError');
  if(!email||!pass){err.textContent='Please fill in all fields.';return;}
  if(!email.includes('@')){err.textContent='Enter a valid email address.';return;}
  if(pass.length<4){err.textContent='Password must be at least 4 characters.';return;}
  state.userName=email.split('@')[0].replace(/[._-]/g,' ').replace(/\b\w/g,c=>c.toUpperCase());
  state.userEmail=email;
  loginSuccess();
}

function handleSignup(){
  const name=document.getElementById('signupName').value.trim();
  const email=document.getElementById('signupEmail').value.trim();
  const pass=document.getElementById('signupPass').value.trim();
  const err=document.getElementById('signupError');
  if(!name||!email||!pass){err.textContent='Please fill in all fields.';return;}
  if(!email.includes('@')){err.textContent='Enter a valid email address.';return;}
  if(pass.length<6){err.textContent='Password must be at least 6 characters.';return;}
  state.userName=name;state.userEmail=email;
  loginSuccess();
}

function loginSuccess(){
  state.loggedIn=true;
  document.getElementById('authScreen').style.display='none';
  document.getElementById('app').classList.add('visible');
  const initials=state.userName.split(' ').map(w=>w[0]).join('').toUpperCase().slice(0,2);
  document.getElementById('navAvatar').textContent=initials;
  document.getElementById('profileAvatar').textContent=initials;
  document.getElementById('lbYouAvatar').textContent=initials;
  document.getElementById('profileName').textContent=state.userName;
  document.getElementById('profEmail').textContent=state.userEmail;
  document.getElementById('lbYouName').textContent=state.userName+' (You)';
  showSection('home');
  showToast('Welcome, '+state.userName+'! 🌿');
}

function handleLogout(){
  state.loggedIn=false;
  if(state.cameraStream)stopCamera();
  document.getElementById('app').classList.remove('visible');
  document.getElementById('authScreen').style.display='flex';
  ['loginEmail','loginPass','signupName','signupEmail','signupPass'].forEach(id=>{const e=document.getElementById(id);if(e)e.value='';});
}

/* ============================================================
   UPDATE UI
============================================================ */
function updateCreditsUI(){
  ['navCredits','dashCredits','walletAmount','profCredits'].forEach(id=>{const e=document.getElementById(id);if(e)e.textContent=state.credits;});
  document.getElementById('walletEarned').textContent=(state.credits+320)+' PC';
  document.getElementById('lbYouPts').textContent=state.credits+' PC';
}
function updateScanCountUI(){
  ['dashScanCount','profScans'].forEach(id=>{const e=document.getElementById(id);if(e)e.textContent=state.scanCount;});
}

/* ============================================================
   CAMERA
============================================================ */
async function startCamera(){
  try{
    const stream=await navigator.mediaDevices.getUserMedia({video:{facingMode:'environment'},audio:false});
    state.cameraStream=stream;
    const v=document.getElementById('videoPreview');
    v.srcObject=stream;v.style.display='block';
    document.getElementById('scanPlaceholder').style.display='none';
    document.getElementById('scanOverlay').style.display='flex';
    document.getElementById('startCamBtn').style.display='none';
    document.getElementById('stopCamBtn').style.display='inline-flex';
    document.getElementById('camStatus').style.display='inline-block';
    showToast('Camera started! 📸');
  }catch(e){showToast('Camera unavailable or permission denied',true);}
}
function stopCamera(){
  if(state.cameraStream){state.cameraStream.getTracks().forEach(t=>t.stop());state.cameraStream=null;}
  document.getElementById('videoPreview').style.display='none';
  document.getElementById('scanPlaceholder').style.display='flex';
  document.getElementById('scanOverlay').style.display='none';
  document.getElementById('startCamBtn').style.display='inline-flex';
  document.getElementById('stopCamBtn').style.display='none';
  document.getElementById('camStatus').style.display='none';
}

/* ============================================================
   DETECT
============================================================ */
function simulateDetect(){
  if(state.detecting)return;
  state.detecting=true;
  document.getElementById('detectResult').classList.remove('show');
  const pick=PLASTICS[Math.floor(Math.random()*PLASTICS.length)];
  setTimeout(()=>{
    document.getElementById('detectedType').textContent=pick.name;
    document.getElementById('confidence').textContent=pick.conf;
    document.getElementById('earnedPts').textContent='+'+pick.pts;
    document.getElementById('detectResult').classList.add('show');
    state.credits+=pick.pts;state.scanCount+=1;
    updateCreditsUI();updateScanCountUI();
    addScanHistory(pick.name,pick.pts);
    showToast('Detected: '+pick.name+' · +'+pick.pts+' Credits 🎉');
    state.detecting=false;
  },900);
}
function addScanHistory(name,pts){
  const list=document.getElementById('scanHistory');
  const item=document.createElement('div');
  item.className='hist-item';
  item.innerHTML=`<i class="fas fa-recycle"></i><div class="hist-info"><div class="name">${name}</div><div class="time">Just now</div></div><div class="hist-pts">+${pts} pts</div>`;
  list.prepend(item);
}

/* ============================================================
   REWARDS
============================================================ */
function redeemReward(cost,name){
  if(state.credits<cost){showToast('Not enough Credits! Need '+cost+' PC',true);return;}
  state.credits-=cost;updateCreditsUI();
  const list=document.getElementById('rewardHistory');
  const item=document.createElement('div');
  item.className='rh-item';
  item.innerHTML=`<span class="rh-desc">Redeemed – ${name}</span><span>Just now</span><span class="rh-pts minus">-${cost} PC</span>`;
  list.prepend(item);
  showToast('🎁 Redeemed: '+name+'!');
}

/* ============================================================
   SMART DUSTBIN
============================================================ */
function simulateDeposit(){
  const PTS=15;
  state.credits+=PTS;state.scanCount+=1;state.binDeposits+=1;
  state.binLevel=Math.min(state.binLevel+5,100);
  updateCreditsUI();updateScanCountUI();
  document.getElementById('binFill').style.height=state.binLevel+'%';
  document.getElementById('binLevelText').textContent=state.binLevel+'%';
  const bc=document.getElementById('binCount');
  bc.textContent=parseInt(bc.textContent)+1;
  const alert=document.getElementById('binAlert');
  if(state.binLevel>=90){alert.className='bin-alert full';alert.textContent='🚨 Bin FULL – Collection Required!';}
  else if(state.binLevel>=70){alert.className='bin-alert warn';alert.textContent='⚠️ Bin getting full ('+state.binLevel+'%)';}
  else{alert.className='bin-alert ok';alert.textContent='● Smart Bin – Block A ('+state.binLevel+'% full)';}
  const log=document.getElementById('depositLog');
  const t=new Date().toLocaleTimeString([],{hour:'2-digit',minute:'2-digit'});
  const types=['PET Bottle','HDPE Cap','Plastic Container','LDPE Bag'];
  const ptype=types[state.binDeposits%types.length];
  const item=document.createElement('div');
  item.className='log-item';
  item.innerHTML=`<span>${ptype} deposited</span><span class="log-time">${t}</span><span class="log-pts">+${PTS} PC</span>`;
  log.prepend(item);
  showToast('Deposit confirmed! +'+PTS+' Plastic Credits 🌿');
}

/* ============================================================
   BAR CHART
============================================================ */
function renderBarChart(){
  const days=['Mon','Tue','Wed','Thu','Fri','Sat','Sun'];
  const vals=[0.4,0.7,0.5,1.1,0.9,1.4,1.2];
  const max=Math.max(...vals);
  const c=document.getElementById('barChart');
  if(!c)return;
  c.innerHTML='';
  days.forEach((d,i)=>{
    const pct=(vals[i]/max)*100;
    c.innerHTML+=`<div class="bar-wrap"><div class="bar" style="height:${pct}%" title="${vals[i]} kg"></div><div class="bar-lbl">${d}</div></div>`;
  });
}

/* ============================================================
   FILTER CHIPS
============================================================ */
document.querySelectorAll('.chip').forEach(chip=>{
  chip.addEventListener('click',function(){
    this.closest('.filter-chips').querySelectorAll('.chip').forEach(c=>c.classList.remove('active'));
    this.classList.add('active');
  });
});

/* ============================================================
   TOAST
============================================================ */
let toastTimer=null;
function showToast(msg,isErr=false){
  const toast=document.getElementById('toast');
  const icon=toast.querySelector('i');
  document.getElementById('toastMsg').textContent=msg;
  icon.className=isErr?'fas fa-exclamation-circle':'fas fa-check-circle';
  icon.style.color=isErr?'#ff8080':'var(--green-light)';
  toast.style.borderColor=isErr?'#ff8080':'var(--green-light)';
  toast.classList.add('show');
  if(toastTimer)clearTimeout(toastTimer);
  toastTimer=setTimeout(()=>toast.classList.remove('show'),3200);
}

/* ============================================================
   INIT
============================================================ */
window.addEventListener('load',()=>{renderBarChart();});
</script>
</body>
</html>
