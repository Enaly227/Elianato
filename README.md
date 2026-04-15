[index.html](https://github.com/user-attachments/files/26760379/index.html)
if(GS.pokerRules)html+='<div class="card"><div class="cl">Reglas del Póker</div><div style="font-size:13px;color:var(--soft);line-height:1.8">'+GS.pokerRules.replace(/\n/g,'<br>')+'</div></div>';<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta http-equiv="Content-Security-Policy" content="upgrade-insecure-requests">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>El Elianato XXVI</title>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;0,700;1,400&family=Cinzel:wght@400;600;900&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#070509;--bg2:#0e0a14;--card:#130d1c;--card2:#1a1028;
  --border:#2e1f4a;--border2:#3d2860;
  --gold:#c9a84c;--gold2:#e8c96a;--gdim:#7a5f20;
  --purple:#7c3aed;--pl:#a855f7;--pdim:#3b1f6e;
  --red:#9b1c3a;--blue:#1d4ed8;--amber:#b45309;
  --text:#f0e8ff;--soft:#c4b8d8;--muted:#7a6a90;--danger:#7f1d1d;
  --ggold:linear-gradient(135deg,#c9a84c,#9a7020);
  --gpurple:linear-gradient(135deg,#2d1b4e,#1a0d2e);
}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{height:100%;background:var(--bg);color:var(--text);font-family:"Cormorant Garamond",serif;font-size:16px;overflow-x:hidden}
body::before{content:"";position:fixed;inset:0;pointer-events:none;z-index:0;opacity:.04;
  background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.75' numOctaves='4'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");}
body::after{content:"";position:fixed;inset:0;pointer-events:none;z-index:0;
  background:radial-gradient(ellipse at 30% 0%,rgba(124,58,237,.12),transparent 60%),
             radial-gradient(ellipse at 70% 100%,rgba(155,28,58,.1),transparent 60%);}
.app{position:relative;z-index:1;display:flex;flex-direction:column;min-height:100dvh;max-width:480px;margin:0 auto}
.pages{flex:1;overflow-y:auto;padding:0 0 80px}
.page{display:none;padding:20px 16px}
.page.active{display:block;animation:fadeUp .3s ease}
@keyframes fadeUp{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:translateY(0)}}

/* SPLASH */
#splash{position:fixed;inset:0;background:var(--bg);z-index:9999;display:flex;flex-direction:column;
  align-items:center;justify-content:center;gap:16px;transition:opacity .8s ease}
#splash.hide{opacity:0;pointer-events:none}
#splash img{width:200px;height:200px;object-fit:contain;
  filter:drop-shadow(0 0 30px rgba(201,168,76,.5));
  animation:coinPulse 2s ease-in-out infinite}
@keyframes coinPulse{0%,100%{filter:drop-shadow(0 0 20px rgba(201,168,76,.3))}
  50%{filter:drop-shadow(0 0 50px rgba(201,168,76,.7)) drop-shadow(0 0 20px rgba(124,58,237,.4))}}
.sptitle{font-family:"Cinzel",serif;font-size:26px;font-weight:900;color:var(--gold);
  letter-spacing:.05em;text-shadow:0 0 30px rgba(201,168,76,.5)}
.spsub{font-size:13px;letter-spacing:.3em;color:var(--muted);font-style:italic}

/* NAV */
.nav{position:fixed;bottom:0;left:50%;transform:translateX(-50%);width:100%;max-width:480px;
  z-index:100;background:rgba(13,9,20,.96);border-top:1px solid var(--border2);
  backdrop-filter:blur(12px);display:flex}
.nb{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;
  padding:9px 2px 13px;background:none;border:none;color:var(--muted);
  font-size:9px;font-family:"Cinzel",serif;letter-spacing:.05em;cursor:pointer;transition:color .2s;gap:3px}
.ni{font-size:18px;transition:transform .2s}
.nb.active{color:var(--gold)}
.nb.active .ni{transform:scale(1.12)}
.nb.locked{opacity:.3;pointer-events:none}
.ni-svg{width:20px;height:20px;flex-shrink:0;transition:transform .2s}
.nb.active .ni-svg{transform:scale(1.12)}

/* CHAT FLOAT BUTTON */
.chat-float{position:fixed;bottom:90px;right:16px;z-index:200;
  background:var(--gpurple);border:1px solid var(--border2);border-radius:50%;
  width:52px;height:52px;display:flex;align-items:center;justify-content:center;
  cursor:pointer;box-shadow:0 4px 20px rgba(124,58,237,.4);transition:all .2s;max-width:calc(480px - 32px)}
.chat-float:hover{transform:scale(1.08);box-shadow:0 6px 28px rgba(124,58,237,.6)}
.chat-float-icon{font-size:22px;line-height:1}
.chat-badge{position:absolute;top:-4px;right:-4px;background:var(--red);color:#fff;
  font-family:"Cinzel",serif;font-size:10px;font-weight:bold;
  border-radius:10px;min-width:18px;height:18px;display:flex;align-items:center;
  justify-content:center;padding:0 4px;border:2px solid var(--bg);
  animation:badgePop .3s ease}
@keyframes badgePop{from{transform:scale(0)}to{transform:scale(1)}}

/* CHAT PANEL (overlay) */
.chat-panel{position:fixed;bottom:0;left:50%;transform:translateX(-50%);
  width:100%;max-width:480px;height:72dvh;max-height:520px;z-index:300;
  background:var(--bg2);border-top:1px solid var(--border2);
  border-radius:16px 16px 0 0;box-shadow:0 -8px 40px rgba(0,0,0,.6);
  display:flex;flex-direction:column;overflow:hidden;transition:transform .3s ease}
.chat-panel.hidden{transform:translateX(-50%) translateY(110%)}
.chat-panel-header{display:flex;align-items:center;justify-content:space-between;
  padding:12px 16px;border-bottom:1px solid var(--border);flex-shrink:0}
.chat-panel-title{font-family:"Cinzel",serif;font-size:14px;color:var(--gold)}
.chat-tabs{display:flex;gap:6px;flex-wrap:wrap;padding:8px 12px;border-bottom:1px solid var(--border);flex-shrink:0}
.chat-tab{font-family:"Cinzel",serif;font-size:10px;letter-spacing:.1em;padding:4px 10px;
  border-radius:12px;border:1px solid var(--border);cursor:pointer;transition:all .2s;
  background:none;color:var(--muted)}
.chat-tab.active{border-color:var(--gold);color:var(--gold);background:rgba(201,168,76,.1)}
.chat-tab .tab-badge{display:inline-block;background:var(--red);color:#fff;
  font-size:9px;border-radius:8px;min-width:14px;height:14px;
  line-height:14px;text-align:center;padding:0 3px;margin-left:3px}
.chat-msgs{flex:1;overflow-y:auto;padding:10px 12px;display:flex;flex-direction:column;gap:7px;min-height:0}
.chat-inp-row{display:flex;gap:7px;padding:8px 12px;border-top:1px solid var(--border);flex-shrink:0}
.chatmsg{display:flex;flex-direction:column;max-width:80%}
.chatmine{align-self:flex-end;align-items:flex-end}
.chauth{font-family:"Cinzel",serif;font-size:8px;letter-spacing:.15em;color:var(--pl);margin-bottom:2px}
.chatmine .chauth{color:var(--gold)}
.chbub{background:var(--card);border:1px solid var(--border);border-radius:10px;
  padding:7px 10px;font-size:14px;color:var(--text);line-height:1.4}
.chatmine .chbub{background:var(--pdim);border-color:var(--purple)}
.chtime{font-size:10px;color:var(--muted);margin-top:2px}
.chat-overlay-bg{position:fixed;inset:0;z-index:290;background:rgba(0,0,0,.5);
  backdrop-filter:blur(2px);transition:opacity .3s}
.chat-overlay-bg.hidden{opacity:0;pointer-events:none}

/* CARDS */
.card{background:var(--card);border:1px solid var(--border);border-radius:8px;padding:16px;margin-bottom:12px}
.acard{background:var(--card);border:1px solid var(--border);border-radius:8px;padding:14px;margin-bottom:10px}
.acard-on{border-color:var(--gold);box-shadow:0 0 20px rgba(201,168,76,.2)}

/* TYPOGRAPHY */
.cl{font-family:"Cinzel",serif;font-size:9px;letter-spacing:.35em;color:var(--pl);text-transform:uppercase;margin-bottom:10px}
.asl{font-size:11px;color:var(--muted);letter-spacing:.15em;margin-bottom:6px;font-family:"Cinzel",serif}
.ahint{font-size:12px;color:var(--muted);margin-bottom:8px;line-height:1.5}
.atitle{font-family:"Cinzel",serif;color:var(--gold);font-size:17px;font-weight:600}
.sec{display:flex;align-items:center;gap:10px;margin:16px 0 10px;
  font-family:"Cinzel",serif;font-size:10px;letter-spacing:.25em;color:var(--muted)}
.sec::before,.sec::after{content:"";flex:1;height:1px;background:linear-gradient(90deg,transparent,var(--border2))}
.gline{height:1px;background:linear-gradient(90deg,transparent,var(--gold),transparent);margin:14px 0}
.ornament{text-align:center;color:var(--gdim);font-size:11px;margin:4px 0 12px}

/* HERO */
.hero{text-align:center;padding:22px 0 8px;background:var(--gpurple);border:1px solid var(--border2);
  border-radius:8px;margin-bottom:14px;position:relative;overflow:hidden;
  box-shadow:0 0 30px rgba(124,58,237,.2)}
.hero::before{content:"";position:absolute;inset:0;
  background:radial-gradient(ellipse at 50% 0%,rgba(201,168,76,.08),transparent 60%);}
.h-eye{font-family:"Cinzel",serif;font-size:7.5px;letter-spacing:.5em;color:var(--pl);margin-bottom:8px}
.h-title{font-family:"Cinzel",serif;font-size:34px;font-weight:900;color:var(--gold);
  letter-spacing:.04em;line-height:1;text-shadow:0 0 40px rgba(201,168,76,.5);margin-bottom:4px}
.h-roman{font-size:11px;letter-spacing:.4em;color:var(--muted);margin-bottom:6px}
.h-tag{font-size:15px;font-style:italic;color:var(--soft);letter-spacing:.08em;padding-bottom:6px}

/* COUNTDOWN */
.cdbox{background:var(--gpurple);border:1px solid var(--border2);border-radius:8px;padding:12px;margin-bottom:12px;text-align:center}
.cdtitle{font-family:"Cinzel",serif;font-size:7.5px;letter-spacing:.4em;color:var(--pl);margin-bottom:8px}
.cdgrid{display:flex;justify-content:center;gap:14px}
.cdu{display:flex;flex-direction:column;align-items:center;gap:1px}
.cdv{font-family:"Cinzel",serif;font-size:24px;font-weight:900;color:var(--gold);line-height:1}
.cdl{font-size:7.5px;letter-spacing:.2em;color:var(--muted);text-transform:uppercase}

/* PROFILE */
.phead{display:flex;align-items:center;gap:12px;padding:12px;background:var(--gpurple);
  border:1px solid var(--border2);border-radius:8px;margin-bottom:12px}
.pav{width:48px;height:48px;border-radius:50%;background:var(--ggold);display:flex;
  align-items:center;justify-content:center;font-family:"Cinzel",serif;font-size:19px;
  font-weight:900;color:#0a0608;flex-shrink:0}
.pname{font-family:"Cinzel",serif;font-size:15px;color:var(--gold);font-weight:600}
.papodo{font-size:13px;color:var(--muted);font-style:italic;margin-top:1px}
.pstats{display:grid;grid-template-columns:repeat(4,1fr);gap:7px;margin-bottom:4px}
.psbox{background:var(--card2);border:1px solid var(--border);border-radius:8px;padding:9px 5px;text-align:center}
.psval{font-family:"Cinzel",serif;font-size:19px;color:var(--gold);font-weight:bold}
.pslbl{font-size:8.5px;color:var(--muted);letter-spacing:.1em;margin-top:1px}
.pfields{display:flex;flex-direction:column;gap:7px}
.pfrow{display:flex;justify-content:space-between;align-items:center;gap:10px;
  padding:5px 0;border-bottom:1px solid var(--border)}
.pflbl{font-size:13px;color:var(--muted);flex-shrink:0;min-width:110px}

/* BTNS */
.btn{display:inline-flex;align-items:center;justify-content:center;gap:6px;
  padding:10px 16px;border-radius:6px;border:none;cursor:pointer;
  font-family:"Cinzel",serif;font-size:12px;letter-spacing:.08em;transition:all .2s;width:100%;margin-top:7px}
.bg{background:var(--ggold);color:#0a0608;font-weight:700;box-shadow:0 4px 14px rgba(201,168,76,.3)}
.bg:hover{filter:brightness(1.1)}
.bgh{background:transparent;color:var(--muted);border:1px solid var(--border2);width:auto}
.bgh:hover{border-color:var(--gold);color:var(--gold)}
.bd{background:var(--danger);color:var(--text)}
.bsm{padding:6px 12px;font-size:11px;margin-top:0}
.bico{background:none;border:none;cursor:pointer;font-size:14px;color:var(--muted);padding:4px;transition:color .2s}
.bico:hover{color:var(--text)}

/* INPUTS */
.inp{width:100%;background:#0c0816;border:1px solid var(--border2);border-radius:6px;
  padding:9px 12px;color:var(--text);font-family:"Cormorant Garamond",serif;font-size:15px;
  outline:none;transition:border-color .2s;margin-top:3px}
.inp:focus{border-color:var(--pl);box-shadow:0 0 0 3px rgba(168,85,247,.1)}
.inp::placeholder{color:var(--muted)}
.insm{padding:5px 8px;font-size:14px}
select.inp{cursor:pointer}
textarea.inp{resize:vertical}
.pin-inp{font-size:18px;letter-spacing:.3em;text-align:center;max-width:130px}

/* SCORES */
.sgrid{display:grid;grid-template-columns:1fr 1fr;gap:9px;margin-bottom:4px}
.sp{background:var(--card2);border:1px solid var(--border);border-radius:8px;padding:10px}
.spt{font-family:"Cinzel",serif;font-size:7.5px;letter-spacing:.3em;color:var(--pl);text-transform:uppercase;margin-bottom:7px}
.sr{display:flex;align-items:center;gap:6px;padding:3px 0;border-bottom:1px solid rgba(46,31,74,.5)}
.sr:last-child{border-bottom:none}
.rn{font-family:"Cinzel",serif;font-size:12px;color:var(--muted);width:16px;text-align:center;flex-shrink:0}
.rn1{color:var(--gold)!important}.rn2{color:#b0b8c8!important}.rn3{color:#cd7f32!important}
.sname{flex:1;font-size:12px;color:var(--soft)}
.spts{font-family:"Cinzel",serif;font-size:12px;color:var(--gold);font-weight:bold}

/* PLAYERS */
.pgrid{display:flex;flex-wrap:wrap;gap:5px;margin-bottom:4px}
.pchip{display:flex;align-items:center;gap:4px;background:var(--card2);
  border:1px solid var(--border);border-radius:20px;padding:3px 9px 3px 6px}
.cnum{font-family:"Cinzel",serif;font-size:10px;color:var(--gold);background:rgba(201,168,76,.1);border-radius:10px;padding:1px 5px}
.cname{font-size:12px;color:var(--soft)}

/* PAGE HEADER */
.phdr{display:flex;align-items:center;justify-content:space-between;margin-bottom:14px}
.ptitle{font-family:"Cinzel",serif;font-size:15px;color:var(--gold);font-weight:600}
.pbadge{font-family:"Cinzel",serif;font-size:8.5px;letter-spacing:.15em;padding:3px 8px;border-radius:12px;border:1px solid}
.bA{color:var(--gold);border-color:var(--gold);background:rgba(201,168,76,.1)}
.bB{color:var(--pl);border-color:var(--pl);background:rgba(168,85,247,.1)}
.bclosed{color:var(--muted);border-color:var(--border)}
.bC{color:#27ae60;border-color:#27ae60;background:rgba(39,174,96,.1)}

/* GUESSES */
.pinfo{font-size:12px;color:var(--muted);font-style:italic;margin-bottom:10px;line-height:1.5;
  padding:7px 10px;background:var(--bg2);border-left:3px solid var(--pdim);border-radius:0 4px 4px 0}
.gc{background:var(--card2);border:1px solid var(--border);border-radius:8px;padding:9px;margin-bottom:7px}
.gc.gg{border-color:#1a4a2a;background:#050f08}
.ghead{display:flex;align-items:center;gap:6px;margin-bottom:7px}
.gnum{font-family:"Cinzel",serif;font-size:10px;color:var(--gold);background:rgba(201,168,76,.1);border-radius:10px;padding:2px 6px}
.gname{flex:1;font-size:14px;color:var(--text)}
.gobadge{font-size:11px;color:#27ae60;background:rgba(39,174,96,.1);border:1px solid rgba(39,174,96,.3);border-radius:4px;padding:2px 6px}
.fopts{display:flex;flex-wrap:wrap;gap:4px;margin-top:3px}
.fo{display:flex;align-items:center;gap:3px;padding:4px 9px;border-radius:20px;
  border:1px solid var(--border);cursor:pointer;font-size:12px;color:var(--muted);
  transition:all .2s;user-select:none}
.fo:hover{border-color:var(--border2);color:var(--text)}
.fo.fsel{border-color:var(--gold);color:var(--gold);background:rgba(201,168,76,.1)}
.fo.fok{border-color:#27ae60;color:#27ae60;background:rgba(39,174,96,.1);font-weight:bold}
.fo.fno{opacity:.35;text-decoration:line-through;pointer-events:none}
.fo.fem{font-size:11px;opacity:.5}
.succ{text-align:center;background:var(--card2);border:1px solid #1a4a2a;border-radius:8px;padding:22px}
.succ-i{font-size:32px;color:#27ae60;margin-bottom:7px}
.succ-t{font-family:"Cinzel",serif;color:var(--gold);font-size:14px;margin-bottom:5px}
.ibox{text-align:center;padding:12px;color:var(--muted);font-style:italic;font-size:13px;
  background:var(--card2);border-radius:8px;border:1px solid var(--border);margin-bottom:9px}
.iok{color:#27ae60;border-color:#1a4a2a;background:#050f08}

/* CLUES */
.clue-box{background:var(--card2);border:1px solid var(--border2);border-radius:8px;padding:12px;margin-bottom:4px}
.clue-title{font-family:"Cinzel",serif;font-size:11px;color:var(--gold);letter-spacing:.15em;margin-bottom:4px}
.clue-item{display:flex;justify-content:space-between;align-items:center;
  padding:5px 0;border-bottom:1px solid var(--border);font-size:13px;color:var(--soft)}

/* MYSTERIES */
.mylist{display:flex;flex-direction:column;gap:8px}
.mycard{background:var(--card2);border:1px solid var(--border2);border-radius:8px;
  padding:12px;cursor:pointer;transition:all .2s;position:relative}
.mycard:hover{border-color:var(--gold);transform:translateY(-1px)}
.mycard.mysolved{border-color:#1a4a2a;background:rgba(5,15,8,.8)}
.mycard-head{display:flex;align-items:center;gap:9px}
.mycard-icon{font-size:22px;flex-shrink:0}
.mycard-info{flex:1}
.mycard-title{font-family:"Cinzel",serif;font-size:13px;color:var(--gold)}
.mycard-meta{font-size:11px;color:var(--muted);margin-top:2px}
.mycard-solvers{font-size:11px;color:#27ae60;margin-top:3px}
.mycard-arrow{color:var(--muted);font-size:16px;flex-shrink:0}

/* MYSTERY DETAIL */
.mydetail{background:var(--card2);border:1px solid var(--border2);border-radius:8px;padding:14px;margin-bottom:8px}
.mydetail-back{display:flex;align-items:center;gap:8px;margin-bottom:12px;cursor:pointer;color:var(--muted);font-size:13px}
.mydetail-back:hover{color:var(--gold)}
.mydetail-progress{display:flex;gap:4px;margin-bottom:12px}
.myprog-dot{height:4px;flex:1;border-radius:2px;background:var(--border)}
.myprog-dot.done{background:var(--gold)}
.myprog-dot.current{background:var(--pl)}
.myclue{font-size:15px;color:var(--soft);line-height:1.7;
  padding:12px;background:var(--bg2);border-left:3px solid var(--pl);
  border-radius:0 6px 6px 0;margin-bottom:12px;font-style:italic}
.myopts{display:flex;flex-direction:column;gap:6px}
.myopt{background:var(--card);border:1px solid var(--border2);border-radius:8px;
  padding:10px 14px;color:var(--text);font-size:14px;cursor:pointer;text-align:left;
  transition:all .2s;font-family:"Cormorant Garamond",serif;width:100%;line-height:1.4}
.myopt:hover{border-color:var(--gold);color:var(--gold);background:rgba(201,168,76,.05)}
.myopt:active{transform:scale(.98)}
.myrev{font-size:14px;color:#27ae60;background:rgba(39,174,96,.08);
  border:1px solid rgba(39,174,96,.3);border-radius:8px;padding:12px 14px;line-height:1.5}

/* REVEAL */
.revcard{display:flex;align-items:center;gap:9px;background:var(--card2);border:1px solid;
  border-radius:8px;padding:9px;margin-bottom:6px;animation:fadeUp .4s ease}
.revnum{font-family:"Cinzel",serif;font-size:14px;color:var(--gold);
  background:rgba(201,168,76,.1);border-radius:10px;padding:2px 8px;flex-shrink:0}
.revname{font-size:14px;color:var(--text);font-weight:600}
.revrole{font-size:12px;font-style:italic;margin-top:1px}

/* POKER */
.hands{background:var(--card2);border:1px solid var(--border);border-radius:8px;overflow:hidden;margin-bottom:10px}
.hrow{display:flex;align-items:center;gap:7px;padding:8px 11px;border-bottom:1px solid rgba(46,31,74,.4)}
.hrow:last-child{border-bottom:none}
.hrk{font-family:"Cinzel",serif;font-size:12px;color:var(--gold);width:18px;text-align:center;flex-shrink:0;font-weight:bold}
.hic{font-size:17px;flex-shrink:0;width:22px;text-align:center}
.hin{flex:1}
.hnm{font-size:13px;color:var(--text);font-weight:600}
.hds{font-size:11px;color:var(--muted);margin-top:1px;font-style:italic}
.tcard{background:var(--card2);border:1px solid var(--border2);border-radius:8px;overflow:hidden;margin-bottom:10px}
.thead{background:var(--gpurple);padding:8px 11px;font-family:"Cinzel",serif;font-size:13px;color:var(--gold)}
.trow{display:flex;justify-content:space-between;align-items:center;
  padding:7px 11px;border-bottom:1px solid rgba(46,31,74,.4);font-size:14px}
.trow:last-child{border-bottom:none}
.tpts{font-family:"Cinzel",serif;font-size:13px;color:var(--gold)}

/* MENU */
.mcard{background:var(--card2);border:1px solid var(--border);border-radius:8px;overflow:hidden;margin-bottom:10px}
.mcat{background:linear-gradient(135deg,rgba(124,58,237,.2),rgba(155,28,58,.15));
  padding:8px 13px;font-family:"Cinzel",serif;font-size:9.5px;letter-spacing:.25em;
  color:var(--gold2);text-transform:uppercase;border-bottom:1px solid var(--border)}
.mitems{padding:9px 13px}
.mitem{display:flex;align-items:center;gap:6px;padding:4px 0;font-size:14px;
  color:var(--soft);border-bottom:1px solid rgba(46,31,74,.3)}
.mitem:last-child{border-bottom:none}
.mdot{color:var(--gdim);font-size:7px;flex-shrink:0}

/* ADMIN TABLE */
.ptbl{border:1px solid var(--border);border-radius:8px;overflow:hidden}
.pthdr{display:grid;grid-template-columns:34px 1fr 44px 1fr 50px;gap:4px;
  padding:6px 9px;background:var(--bg2);font-family:"Cinzel",serif;font-size:8px;letter-spacing:.2em;color:var(--muted)}
.ptrow{display:grid;grid-template-columns:34px 1fr 44px 1fr 50px;gap:4px;
  padding:7px 9px;border-top:1px solid var(--border);font-size:13px;align-items:center}
.ptrow:hover{background:var(--bg2)}
.ptnum{font-family:"Cinzel",serif;color:var(--gold);font-size:11px}
.ptcode{font-family:"Cinzel",serif;color:var(--pl);font-size:11px}
.ptacts{display:flex;gap:3px;justify-content:flex-end}

/* RESULTS */
.resrow{display:flex;align-items:center;gap:6px;padding:5px 0;border-bottom:1px solid var(--border)}
.sublbl{font-size:10px;color:var(--pl);margin:3px 0 2px 20px;font-family:"Cinzel",serif;letter-spacing:.1em}
.subdet{font-size:12px;margin-left:20px;margin-bottom:2px;display:flex;gap:4px;flex-wrap:wrap}
.subtgt{color:var(--muted)}
.ok{color:#27ae60}.err{color:#e74c3c}.muted{color:var(--muted)}

/* MISC */
.msg{font-size:13px;margin-top:7px;min-height:15px}
.lok{position:fixed;inset:0;background:rgba(0,0,0,.85);z-index:400;
  display:flex;align-items:center;justify-content:center}
.lokcard{background:var(--card);border:1px solid rgba(201,168,76,.3);
  border-radius:8px;padding:26px;width:285px;text-align:center}
.lscreen{text-align:center;padding:70px 20px}
.licon{font-size:42px;margin-bottom:12px;opacity:.6}
.lmsg{font-family:"Cinzel",serif;color:var(--gold);font-size:13px;letter-spacing:.1em;line-height:1.6}
.divrow{display:flex;align-items:center;gap:8px;margin:10px 0}
.divl{flex:1;height:1px;background:var(--border)}
.divd{color:var(--gdim);font-size:9px}
.report-btn{background:none;border:none;cursor:pointer;font-size:12px;color:var(--muted);
  padding:2px 7px;border-radius:4px;border:1px solid var(--border);transition:all .2s;margin-top:5px}
.report-btn:hover{color:var(--red);border-color:var(--red)}
.myslvrow{display:flex;justify-content:space-between;align-items:center;
  padding:5px 0;border-bottom:1px solid var(--border);font-size:13px}
.tglrow{display:flex;justify-content:space-between;align-items:center;
  padding:7px 0;font-size:13px;cursor:pointer;border-bottom:1px solid var(--border)}
.ctrlgrid{display:grid;grid-template-columns:1fr 1fr;gap:12px}
.role-card{background:linear-gradient(135deg,var(--card2),#0d0820);border:1px solid var(--gold);border-radius:9px;padding:14px;margin-bottom:12px}
.role-priv-lbl{font-size:8px;letter-spacing:.28em;color:var(--muted);font-family:"Cinzel",serif;margin-bottom:5px;text-transform:uppercase}
.role-nm{font-family:"Cinzel",serif;font-size:18px;color:var(--gold);font-weight:900;margin-bottom:3px}
.role-fc{font-size:11px;letter-spacing:.18em;margin-bottom:9px}
.role-ds{font-size:13px;color:var(--soft);line-height:1.7;margin-bottom:12px;border-left:2px solid var(--gold);padding-left:9px;font-style:italic}
.pwbtn{background:linear-gradient(135deg,#2d1b4e,#1a0d30);border:1px solid var(--pl);border-radius:7px;padding:10px 14px;width:100%;cursor:pointer;text-align:left;transition:all .18s;font-family:inherit}
.pwbtn:hover{border-color:var(--gold);box-shadow:0 0 14px rgba(201,168,76,.18)}
.pwbtn.used{opacity:.45;border-color:var(--border);cursor:not-allowed}
.pw-nm{font-family:"Cinzel",serif;font-size:11px;color:var(--pl);letter-spacing:.12em;margin-bottom:3px}
.pw-st{font-size:12px;color:var(--muted)}
.amsg{background:#0a0614;border-left:3px solid var(--gold);padding:9px 11px;margin-bottom:6px;border-radius:0 5px 5px 0;cursor:pointer}
.amsg.afalse{border-left-color:var(--red)}
.amsg-tx{font-size:13px;color:var(--soft);line-height:1.5;font-style:italic}
.amsg-fa{font-size:9px;color:var(--red);margin-top:3px}
.scgrid{display:grid;grid-template-columns:1fr 1fr;gap:6px;margin-bottom:8px}
.scfield{display:flex;flex-direction:column;gap:2px}
.sclbl{font-size:10px;color:var(--muted)}
.role-card{background:linear-gradient(135deg,var(--card2),#0d0820);border:1px solid var(--gold);border-radius:9px;padding:14px;margin-bottom:12px}
.role-priv-lbl{font-size:8px;letter-spacing:.28em;color:var(--muted);font-family:"Cinzel",serif;margin-bottom:5px;text-transform:uppercase}
.role-nm{font-family:"Cinzel",serif;font-size:18px;color:var(--gold);font-weight:900;margin-bottom:3px}
.role-fc{font-size:11px;letter-spacing:.18em;margin-bottom:9px}
.role-ds{font-size:13px;color:var(--soft);line-height:1.7;margin-bottom:12px;border-left:2px solid var(--gold);padding-left:9px;font-style:italic}
.pwbtn{background:linear-gradient(135deg,#2d1b4e,#1a0d30);border:1px solid var(--pl);border-radius:7px;padding:10px 14px;width:100%;cursor:pointer;text-align:left;transition:all .18s;font-family:inherit}
.pwbtn:hover{border-color:var(--gold);box-shadow:0 0 14px rgba(201,168,76,.18)}
.pwbtn.used{opacity:.45;border-color:var(--border);cursor:not-allowed}
.pw-nm{font-family:"Cinzel",serif;font-size:11px;color:var(--pl);letter-spacing:.12em;margin-bottom:3px}
.pw-st{font-size:12px;color:var(--muted)}
.amsg{background:#0a0614;border-left:3px solid var(--gold);padding:9px 11px;margin-bottom:6px;border-radius:0 5px 5px 0}
.amsg.afalse{border-left-color:var(--red)}
.amsg-tx{font-size:13px;color:var(--soft);line-height:1.5;font-style:italic}
.amsg-fa{font-size:9px;color:var(--red);margin-top:3px}
.scgrid{display:grid;grid-template-columns:1fr 1fr;gap:6px;margin-bottom:8px}
.scfield{display:flex;flex-direction:column;gap:2px}
.sclbl{font-size:10px;color:var(--muted)}
.hand-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:9px}
.hand-card{background:var(--card2);border:1px solid var(--border);border-radius:10px;padding:10px 11px;position:relative;overflow:hidden;transition:border-color .2s}
.hand-card:hover{border-color:var(--gold)}
.hand-card::before{content:"";position:absolute;top:0;left:0;right:0;height:2px;border-radius:2px 2px 0 0}
.hand-r1::before{background:linear-gradient(90deg,#f59e0b,#fbbf24)}
.hand-r2::before{background:linear-gradient(90deg,#6366f1,#8b5cf6)}
.hand-r3::before{background:linear-gradient(90deg,#10b981,#34d399)}
.hand-r4::before{background:linear-gradient(90deg,#ec4899,#f472b6)}
.hand-r5::before,.hand-r6::before{background:linear-gradient(90deg,#3b82f6,#60a5fa)}
.hand-r7::before,.hand-r8::before{background:linear-gradient(90deg,#8b5cf6,#a78bfa)}
.hand-r9::before,.hand-r10::before{background:var(--border2)}
.hand-rank{font-family:"Cinzel",serif;font-size:9px;color:var(--muted);letter-spacing:.15em;margin-bottom:3px}
.hand-name{font-family:"Cinzel",serif;font-size:12px;color:var(--gold);font-weight:600;margin-bottom:2px}
.hand-desc{font-size:10px;color:var(--soft);line-height:1.4}
.hand-ex{font-size:13px;letter-spacing:2px;color:var(--muted);margin-top:4px}
.hand-badge{position:absolute;top:8px;right:8px;font-size:9px;font-family:"Cinzel",serif;letter-spacing:.08em;padding:1px 6px;border-radius:10px;border:1px solid}
::-webkit-scrollbar{width:3px}
::-webkit-scrollbar-track{background:var(--bg)}
::-webkit-scrollbar-thumb{background:var(--border2);border-radius:2px}
/* REFINED DESIGN */
.card,.acard{box-shadow:0 2px 20px rgba(0,0,0,.3)}
.hero{box-shadow:0 4px 40px rgba(124,58,237,.25),inset 0 1px 0 rgba(201,168,76,.1)}
.tcard{box-shadow:0 2px 16px rgba(0,0,0,.3)}
.nb span{font-size:8.5px;letter-spacing:.08em}
/* PLAYER CHIP HOVER */
.pchip{transition:all .15s}
.pchip:hover{border-color:var(--gold);background:rgba(201,168,76,.06)}
/* SECTION DIVIDER MORE REFINED */
.sec{margin:18px 0 12px;font-size:9px;letter-spacing:.3em}
/* MYSTERY CARD REFINED */
.mycard{transition:border-color .2s,box-shadow .2s}
.mycard:hover{box-shadow:0 4px 20px rgba(124,58,237,.2)}
/* SCORE PANELS */
.sp{box-shadow:0 2px 16px rgba(0,0,0,.25)}
/* BETTER BADGE */
.chat-badge{font-size:10px;font-family:"Cinzel",serif;font-weight:900;letter-spacing:0}
</style>
</head>
<body>

<!-- SPLASH -->
<div id="splash">
  <img src="data:image/webp;base64,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" alt="El Elianato">
  <div class="sptitle">El Elianato</div>
  <div class="spsub">XXVI · Intereses Cruzados</div>
</div>

<div class="app">
  <div class="pages">
    <div class="page active" id="p1"><div id="p1c"></div></div>
    <div class="page" id="p2"><div id="p2c"></div></div>
    <div class="page" id="p3"><div id="p3c"></div></div>
    <div class="page" id="p4"><div id="p4c"></div></div>
    <div class="page" id="admin"><div id="admc"></div></div>
  </div>
  <nav class="nav">
    <button class="nb active" data-page="p1" onclick="nav('p1')">
      <svg class="ni-svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><circle cx="12" cy="8" r="4"/><path d="M4 20c0-4 3.6-7 8-7s8 3 8 7"/></svg>
      <span>Inicio</span>
    </button>
    <button class="nb" data-page="p2" onclick="nav('p2')">
      <svg class="ni-svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><circle cx="11" cy="11" r="7"/><path d="M16.5 16.5L21 21"/><path d="M8 11h6M11 8v6"/></svg>
      <span>Juego</span>
    </button>
    <button class="nb" data-page="p3" onclick="nav('p3')">
      <svg class="ni-svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="2" y="6" width="20" height="14" rx="2"/><path d="M6 6V4a2 2 0 014 0v2M14 6V4a2 2 0 014 0v2"/><circle cx="8" cy="13" r="1.5" fill="currentColor"/><circle cx="12" cy="13" r="1.5" fill="currentColor"/><circle cx="16" cy="13" r="1.5" fill="currentColor"/></svg>
      <span>Mesas</span>
    </button>
    <button class="nb" data-page="p4" onclick="nav('p4')">
      <svg class="ni-svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M12 2C6.5 2 2 6.5 2 12s4.5 10 10 10 10-4.5 10-10S17.5 2 12 2z"/><path d="M2 12h20M12 2a15.3 15.3 0 014 10 15.3 15.3 0 01-4 10 15.3 15.3 0 01-4-10 15.3 15.3 0 014-10z"/></svg>
      <span>Catering</span>
    </button>
  </nav>
</div>

<!-- CHAT FLOAT -->
<div class="chat-float" id="chat-fab" onclick="openChatPanel()" style="display:none">
  <svg style="width:22px;height:22px;stroke:currentColor;fill:none;stroke-width:1.8" viewBox="0 0 24 24">
    <path d="M21 15a2 2 0 01-2 2H7l-4 4V5a2 2 0 012-2h14a2 2 0 012 2z" stroke-linejoin="round" stroke-linecap="round"/>
  </svg>
  <div class="chat-badge" id="chat-badge" style="display:none">0</div>
</div>

<!-- CHAT OVERLAY BG -->
<div class="chat-overlay-bg hidden" id="chat-overlay" onclick="closeChatPanel()"></div>

<!-- CHAT PANEL -->
<div class="chat-panel hidden" id="chat-panel">
  <div class="chat-panel-header">
    <div class="chat-panel-title">💬 Chat</div>
    <button class="bico" onclick="closeChatPanel()" style="font-size:20px">✕</button>
  </div>
  <div class="chat-tabs" id="chat-tabs"></div>
  <div class="chat-msgs" id="chat-msgs"></div>
  <div class="chat-inp-row" id="chat-inp-row"></div>
</div>

<!-- ADMIN LOGIN MODAL -->
<div class="lok" id="admin-modal" style="display:none">
  <div class="lokcard">
    <div style="font-size:30px;margin-bottom:8px">🔐</div>
    <div style="font-family:Cinzel,serif;color:var(--gold);font-size:16px;margin-bottom:14px">Organizador</div>
    <input class="inp" id="apin" type="password" placeholder="PIN" style="text-align:center;letter-spacing:.3em">
    <button class="btn bg" onclick="doAdminLogin()" style="margin-top:8px">Entrar</button>
    <button class="bgh bsm" onclick="hideAdminModal()" style="margin-top:7px;width:100%">Cancelar</button>
    <div id="apin-msg" class="msg"></div>
  </div>
</div>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
import { getDatabase,ref,set,get,onValue,push,remove,update }
  from "https://www.gstatic.com/firebasejs/10.12.0/firebase-database.js";

const FC={
  apiKey:"AIzaSyCcfQMsjaEnaoVIPonw-OMFMDWQGrDJJOg",
  authDomain:"elianato-3.firebaseapp.com",
  databaseURL:"https://elianato-2026-default-rtdb.firebaseio.com",
  projectId:"elianato-3",
  storageBucket:"elianato-3.firebasestorage.app",
  messagingSenderId:"567908048635",
  appId:"1:567908048635:web:2df8874ab093ab18675a5e"
};
const fa=initializeApp(FC);
const db=getDatabase(fa);
const dg=async p=>{const s=await get(ref(db,p));return s.val();};
const ds=(p,v)=>set(ref(db,p),v);
const du=(p,v)=>update(ref(db,p),v);
const dp=(p,v)=>push(ref(db,p),v);
const dd=p=>remove(ref(db,p));
const dl=(p,cb)=>onValue(ref(db,p),s=>cb(s.val()));
const norm=s=>s?s.toLowerCase().normalize("NFD").replace(/[\u0300-\u036f]/g,"").trim():"";

const ROLES_INFO={"El Padrino": {"fac": "La Familia", "tipo": "Protector", "poder": "Protección", "desc": "Elegí a un aliado (no a vos mismo). Al cerrar la fase, si alguien de su misma facción acertó su rol, esas penalizaciones se anulan. Regla global: los puntos negativos entre miembros de la misma facción siempre se cancelan. 1 uso por fase."}, "El Soplón": {"fac": "La Familia", "tipo": "Informante", "poder": "Red de datos", "desc": "Elegí entre tres acciones: ver las pistas registradas de un jugador, confirmar la facción de un número de collar (la info le llega a un aliado tuyo al azar), o confirmar el rol de 1 jugador (El Fantasma no puede ser confirmado). 1 uso por acción."}, "El Sicario": {"fac": "La Familia", "tipo": "Atacante A", "poder": "Bloqueo de misterios", "desc": "Bloqueás a un jugador de resolver misterios por 15 min. Recibe un aviso del sistema y un contador. 2 usos."}, "El Consigliere": {"fac": "La Familia", "tipo": "Todoterreno", "poder": "Estratega", "desc": "Elegí entre dos acciones: compartir un misterio resuelto con toda tu facción, o pedirle una pista a otro jugador (él decide si la da y cuál). 1 uso."}, "El Prestamista": {"fac": "La Familia", "tipo": "Comodín", "poder": "Duelo de puntos", "desc": "Elegí a un jugador sin ninguna pista tuya. Si adivinás su facción → 5% de sus puntos. Si adivinás facción Y rol → 15%. Máx 2 duelos."}, "El Músico": {"fac": "La Familia", "tipo": "Reserva", "poder": "—", "desc": "Este rol no tiene habilidad esta noche."}, "El Director": {"fac": "Agencia", "tipo": "Protector", "poder": "Protección", "desc": "Elegí a un aliado (no a vos mismo). Al cerrar la fase, si alguien de su misma facción acertó su rol, esas penalizaciones se anulan. Regla global: los puntos negativos entre miembros de la misma facción siempre se cancelan. 1 uso por fase."}, "El Infiltrado": {"fac": "Agencia", "tipo": "Informante", "poder": "Red de datos", "desc": "Elegí entre tres acciones: ver las pistas registradas de un jugador, confirmar la facción de un número de collar (la info le llega a un aliado tuyo al azar), o confirmar el rol de 1 jugador (El Fantasma no puede ser confirmado). 1 uso por acción."}, "El Saboteador": {"fac": "Agencia", "tipo": "Atacante B", "poder": "Pista falsa", "desc": "Plantás una pista falsa al azar en el registro de hasta 2 jugadores. La ven como escrita por ellos mismos. 1 uso."}, "El Analista": {"fac": "Agencia", "tipo": "Todoterreno", "poder": "Estratega", "desc": "Elegí entre dos acciones: compartir un misterio resuelto con toda tu facción, o pedirle una pista a otro jugador (él decide si la da y cuál). 1 uso."}, "El Camaleón": {"fac": "Agencia", "tipo": "Comodín", "poder": "Copia de poder", "desc": "Copiás el poder de cualquier jugador que no sea otro Comodín. Podés usarlo 1 vez. El dueño recibe alerta anónima. 1 vez por fase."}, "El Poeta": {"fac": "Agencia", "tipo": "Reserva", "poder": "—", "desc": "Este rol no tiene habilidad esta noche."}, "El Intendente": {"fac": "El Concejo", "tipo": "Protector", "poder": "Protección", "desc": "Elegí a un aliado (no a vos mismo). Al cerrar la fase, si alguien de su misma facción acertó su rol, esas penalizaciones se anulan. Regla global: los puntos negativos entre miembros de la misma facción siempre se cancelan. 1 uso por fase."}, "El Fiscal": {"fac": "El Concejo", "tipo": "Informante", "poder": "Red de datos", "desc": "Elegí entre tres acciones: ver las pistas registradas de un jugador, confirmar la facción de un número de collar (la info le llega a un aliado tuyo al azar), o confirmar el rol de 1 jugador (El Fantasma no puede ser confirmado). 1 uso por acción."}, "El Censor": {"fac": "El Concejo", "tipo": "Atacante C", "poder": "Propaganda", "desc": "Enviás pistas a hasta 4 jugadores. El sistema decide 50/50 si cada una llega verdadera o falsa. El destinatario puede verlo. 1 uso."}, "El Delegado": {"fac": "El Concejo", "tipo": "Todoterreno", "poder": "Estratega", "desc": "Elegí entre dos acciones: compartir un misterio resuelto con toda tu facción, o pedirle una pista a otro jugador (él decide si la da y cuál). 1 uso."}, "El Ministro": {"fac": "El Concejo", "tipo": "Comodín", "poder": "Multiplicador", "desc": "Elegí a un aliado. Sus puntos de la fase activa se duplican (máx +8 pts). El aliado no lo sabe hasta ver sus puntos. 1 uso."}, "El Artista": {"fac": "El Concejo", "tipo": "Reserva", "poder": "—", "desc": "Este rol no tiene habilidad esta noche."}, "El Dictador": {"fac": "Los Únicos", "tipo": "Protector", "poder": "Protección", "desc": "Elegí a un aliado (no a vos mismo). Al cerrar la fase, si alguien de su misma facción acertó su rol, esas penalizaciones se anulan. Regla global: los puntos negativos entre miembros de la misma facción siempre se cancelan. 1 uso por fase."}, "El Cronista": {"fac": "Los Únicos", "tipo": "Informante", "poder": "Red de datos", "desc": "Elegí entre tres acciones: ver las pistas registradas de un jugador, confirmar la facción de un número de collar (la info le llega a un aliado tuyo al azar), o confirmar el rol de 1 jugador (El Fantasma no puede ser confirmado). 1 uso por acción."}, "El Agitador": {"fac": "Los Únicos", "tipo": "Atacante D", "poder": "Borrado", "desc": "Eliminás hasta 2 pistas del registro de un jugador. Ese jugador pierde esa información sin saber quién fue. 1 uso."}, "El Navegante": {"fac": "Los Únicos", "tipo": "Todoterreno", "poder": "Estratega", "desc": "Elegí entre dos acciones: compartir un misterio resuelto con toda tu facción, o pedirle una pista a otro jugador (él decide si la da y cuál). 1 uso."}, "El Fantasma": {"fac": "Los Únicos", "tipo": "Comodín", "poder": "Inmunidad total", "desc": "Sos inmune a todos los efectos negativos. Si alguien te ataca, recibís una alerta sin saber quién fue. Los Informantes no pueden confirmarte."}, "El Viajero": {"fac": "Los Únicos", "tipo": "Reserva", "poder": "—", "desc": "Este rol no tiene habilidad esta noche."}};
const ROLES_PRESET=[{"nombre": "El Padrino", "fac": "La Familia", "tipo": "Protector"}, {"nombre": "El Soplón", "fac": "La Familia", "tipo": "Informante"}, {"nombre": "El Sicario", "fac": "La Familia", "tipo": "Atacante A"}, {"nombre": "El Consigliere", "fac": "La Familia", "tipo": "Todoterreno"}, {"nombre": "El Prestamista", "fac": "La Familia", "tipo": "Comodín"}, {"nombre": "El Músico", "fac": "La Familia", "tipo": "Reserva"}, {"nombre": "El Director", "fac": "Agencia", "tipo": "Protector"}, {"nombre": "El Infiltrado", "fac": "Agencia", "tipo": "Informante"}, {"nombre": "El Saboteador", "fac": "Agencia", "tipo": "Atacante B"}, {"nombre": "El Analista", "fac": "Agencia", "tipo": "Todoterreno"}, {"nombre": "El Camaleón", "fac": "Agencia", "tipo": "Comodín"}, {"nombre": "El Poeta", "fac": "Agencia", "tipo": "Reserva"}, {"nombre": "El Intendente", "fac": "El Concejo", "tipo": "Protector"}, {"nombre": "El Fiscal", "fac": "El Concejo", "tipo": "Informante"}, {"nombre": "El Censor", "fac": "El Concejo", "tipo": "Atacante C"}, {"nombre": "El Delegado", "fac": "El Concejo", "tipo": "Todoterreno"}, {"nombre": "El Ministro", "fac": "El Concejo", "tipo": "Comodín"}, {"nombre": "El Artista", "fac": "El Concejo", "tipo": "Reserva"}, {"nombre": "El Dictador", "fac": "Los Únicos", "tipo": "Protector"}, {"nombre": "El Cronista", "fac": "Los Únicos", "tipo": "Informante"}, {"nombre": "El Agitador", "fac": "Los Únicos", "tipo": "Atacante D"}, {"nombre": "El Navegante", "fac": "Los Únicos", "tipo": "Todoterreno"}, {"nombre": "El Fantasma", "fac": "Los Únicos", "tipo": "Comodín"}, {"nombre": "El Viajero", "fac": "Los Únicos", "tipo": "Reserva"}];
const DEFAULT_CLUES={"comun": ["El jugador #N y el jugador #M están en la misma facción.", "El jugador #N no pertenece a La Familia.", "El jugador #N no pertenece a la facción más grande de esta noche.", "El jugador #N tiene una habilidad activa (no es Reserva).", "El jugador #N es aliado del jugador #M.", "El jugador #N y el jugador #M son rivales (distintas facciones).", "El jugador #N no es el líder de su facción.", "El jugador #N es de una facción con exactamente 6 miembros.", "Hay al menos un miembro de El Concejo entre los jugadores #N y #M.", "El jugador #N comparte facción con exactamente 2 personas en esta mesa.", "El jugador #N y el jugador #M nunca podrían ser protegidos por el mismo Protector.", "El jugador #N tiene la misma facción que el jugador #M."], "pocoComun": ["El jugador #N pertenece a Agencia.", "El jugador #N pertenece a El Concejo.", "El jugador #N no pertenece ni a La Familia ni a Agencia.", "El jugador #N tiene capacidad de bloquear a otros jugadores esta noche.", "El jugador #N puede ver las pistas de otro jugador sin que lo sepa.", "El jugador #N puede enviar información falsa como si fuera real.", "El jugador #N tiene un rol de protección.", "El jugador #N es el Informante de su facción.", "El jugador #N puede transferir puntos de otro jugador a sí mismo.", "El jugador #N puede copiar la habilidad de otro rol.", "El jugador #N, #M y #P pertenecen a tres facciones distintas.", "El jugador #N tiene un poder que puede usarse tanto en Fase A como en Fase B."], "rara": ["El jugador #N pertenece a La Familia.", "El jugador #N pertenece a Los Únicos.", "El jugador #N es el Comodín de su facción.", "El jugador #N y el jugador #M son los dos Protectores de sus respectivas facciones.", "El jugador #N tiene inmunidad a todos los efectos negativos del juego.", "El jugador #N puede duplicar los puntos de un aliado al final de la fase.", "El jugador #N ya activó su poder esta noche.", "El jugador #N aún no usó su poder.", "El jugador #N tiene el rol de Todoterreno en su facción.", "El jugador #N puede hacer que un misterio resuelto se comparta con toda su facción.", "El jugador #N pertenece a la facción con el nombre más largo.", "El jugador #N es atacante y ya usó uno de sus dos usos."], "especial": ["El jugador #N tiene el rol [ROL].", "El jugador #N pertenece a la facción [FACCION].", "El jugador #N y el jugador #M son ambos de La Familia.", "Los jugadores #N, #M y #P son los tres líderes de sus facciones.", "El jugador #N es El Fantasma: inmune a todo ataque.", "El jugador #N puede robarte puntos si no tenés pistas sobre él.", "El jugador #N protegerá a alguien esta noche.", "El jugador #N plantó una pista falsa en el registro de alguien.", "Estos cuatro jugadores son los Comodines: #N, #M, #P y #Q.", "El jugador #N intentó atacar a El Fantasma y falló.", "El jugador #N recibió una pista falsa sin saberlo.", "El jugador #N usó su poder de Copia y tomó la habilidad de otro rol."]};

const CAN_SEND_FALSE=['Tesorero','Enlace','Periodista','Escritor','Chofer'];
const DEFAULT_PTS={fA:2,fF:-0.5,fOA:-0.5,fOF:0.5,rA:5,rF:-2,rOA:-1,rOF:1};
function getPTS(){return GS.ptsConfig||DEFAULT_PTS;}


let CU=null,CP='p1',GS={};
// Cache global de datos en tiempo real
let PLAYERS={},SUBS={},TABLES={},CHATS={};
const PTS={fo:2,ff:-.5,ro:5,rf:-2};
const FACS=['La Familia','Agencia','El Concejo','Los Únicos'];
const FI={'La Familia':'♦','Mafia':'♦','Agencia':'◈','El Concejo':'⬡','Municipales':'⬡','Los Únicos':'★','Especial':'★'};
const FC2={'La Familia':'var(--red)','Mafia':'var(--red)','Agencia':'var(--blue)','El Concejo':'var(--amber)','Municipales':'var(--amber)','Los Únicos':'var(--pur)','Especial':'var(--pur)'};
const APODOS=['El Zurdo', 'La Sombra', 'El Fantasma', 'El Silencioso', 'La Serpiente', 'El Lobo', 'La Araña', 'El Halcón', 'El Toro', 'La Hiena', 'El Cuervo', 'La Víbora', 'El Oso', 'El Escorpión', 'El Tiburón'];
let chatActiveCid='global';
let unreadPrivate={};
let lastSeenTs={};

// ── BOOT ─────────────────────────────────────────────
window.addEventListener('DOMContentLoaded',async()=>{
  setTimeout(()=>{
    const s=document.getElementById('splash');
    s.classList.add('hide');
    setTimeout(()=>s.style.display='none',850);
  },2000);

  const pin=await dg('config/pin');
  if(!pin)await ds('config/pin','1234');

  // Listeners globales en tiempo real — se registran una sola vez
  dl('gamestate',val=>{GS=val||{};renderAll();});
  dl('players',val=>{PLAYERS=val||{};if(CP==='p2')rP2();if(CP==='p3')rP3();});
  dl('submissions',val=>{SUBS=val||{};if(CP==='p2')rP2();});
  dl('tables',val=>{TABLES=val||{};if(CP==='p3')rP3();});

  const saved=localStorage.getItem('eu');
  if(saved){try{CU=JSON.parse(saved);}catch(e){}}
  rp('p1');
});

// ── NAV ───────────────────────────────────────────────
const isOn=p=>GS.testMode||GS.enabled?.[p];

window.nav=page=>{
  if(['p2','p3','p4'].includes(page)&&!isOn(page))return;
  CP=page;
  document.querySelectorAll('.page').forEach(x=>x.classList.remove('active'));
  document.querySelectorAll('.nb').forEach(x=>x.classList.remove('active'));
  document.getElementById(page)?.classList.add('active');
  document.querySelector(`.nb[data-page="${page}"]`)?.classList.add('active');
  rp(page);
};

function renderAll(){updateNav();rp(CP);}
function updateNav(){
  document.querySelectorAll('.nb').forEach(b=>{
    const pg=b.dataset.page;
    b.classList.toggle('locked',['p2','p3','p4'].includes(pg)&&!isOn(pg));
  });
  // Mostrar/ocultar chat fab
  const fab=document.getElementById('chat-fab');
  if(fab)fab.style.display=(CU&&!CU.isAdmin&&isOn('p2'))?'flex':'none';
}

// ── ADMIN MODAL ───────────────────────────────────────
window.showAdminModal=()=>{
  document.getElementById('admin-modal').style.display='flex';
  document.getElementById('apin').value='';
  document.getElementById('apin-msg').innerHTML='';
};
window.hideAdminModal=()=>document.getElementById('admin-modal').style.display='none';
window.doAdminLogin=async()=>{
  const pin=document.getElementById('apin').value.trim();
  const real=await dg('config/pin');
  if(pin===real){
    CU={name:'Admin',isAdmin:true};
    localStorage.setItem('eu',JSON.stringify(CU));
    hideAdminModal();
    nav('admin');
  } else {
    document.getElementById('apin-msg').innerHTML='<span class="err">PIN incorrecto.</span>';
  }
};

function rp(page){
  if(page==='p1')rP1();
  else if(page==='p2')rP2();
  else if(page==='p3')rP3();
  else if(page==='p4')rP4();
  else if(page==='admin')rAdmin();
}

// ── CHAT PANEL ────────────────────────────────────────
let chatListeners={};
let chatPanelOpen=false;

window.openChatPanel=()=>{
  document.getElementById('chat-panel').classList.remove('hidden');
  document.getElementById('chat-overlay').classList.remove('hidden');
  chatPanelOpen=true;
  buildChatTabs();
  switchChatTab(chatActiveCid);
};
window.closeChatPanel=()=>{
  document.getElementById('chat-panel').classList.add('hidden');
  document.getElementById('chat-overlay').classList.add('hidden');
  chatPanelOpen=false;
};

function buildChatTabs(){
  const tabs=document.getElementById('chat-tabs');
  if(!tabs)return;
  const entries=Object.values(PLAYERS).filter(p=>p.name&&CU&&norm(p.name)!==norm(CU.name));
  let html=`<button class="chat-tab ${chatActiveCid==='global'?'active':''}" onclick="window.switchChatTab('global')">Global</button>`;
  entries.forEach(p=>{
    const cid='priv_'+[CU.name,p.name].sort().join('_');
    const unread=unreadPrivate[cid]||0;
    html+=`<button class="chat-tab ${chatActiveCid===cid?'active':''}" onclick="window.switchChatTab('${cid}')">
      ${p.name}${unread>0?`<span class="tab-badge">${unread}</span>`:''}
    </button>`;
  });
  tabs.innerHTML=html;
}

function switchChatTab(cid){
  chatActiveCid=cid;
  if(cid!=='global'){
    lastSeenTs[cid]=Date.now();
    unreadPrivate[cid]=0;
    updateBadge();
  }
  buildChatTabs();
  const msgsEl=document.getElementById('chat-msgs');
  const inpEl=document.getElementById('chat-inp-row');
  if(!msgsEl||!inpEl)return;
  msgsEl.innerHTML='<div style="color:var(--muted);font-size:13px;text-align:center;padding:14px">Cargando...</div>';
  inpEl.innerHTML=CU&&!CU.isAdmin?`
    <input class="inp" id="chat-inp" placeholder="Escribí un mensaje..." style="margin-top:0;flex:1"
      onkeydown="if(event.key==='Enter'){event.preventDefault();window.sendChat();}">
    <button class="btn bg bsm" onclick="window.sendChat()" style="margin-top:0;width:auto;flex-shrink:0">Enviar</button>`:'';

  if(!chatListeners[cid]){
    chatListeners[cid]=dl('chats/'+cid,msgs=>{
      CHATS[cid]=msgs||{};
      if(chatPanelOpen&&chatActiveCid===cid)renderChatMsgs(cid);
      else if(cid!=='global'&&msgs){
        // contar no leídos
        const seen=lastSeenTs[cid]||0;
        const unread=Object.values(msgs).filter(m=>m.ts>seen&&m.author!==CU?.name).length;
        unreadPrivate[cid]=unread;
        updateBadge();
        if(chatPanelOpen)buildChatTabs();
      }
    });
  } else {
    renderChatMsgs(cid);
  }
}

function renderChatMsgs(cid){
  const el=document.getElementById('chat-msgs');if(!el)return;
  const msgs=CHATS[cid]||{};
  const sorted=Object.values(msgs).sort((a,b)=>a.ts-b.ts);
  if(!sorted.length){el.innerHTML='<div style="color:var(--muted);font-size:13px;text-align:center;padding:14px">Sin mensajes.</div>';return;}
  el.innerHTML=sorted.map(m=>`<div class="chatmsg ${CU&&m.author===CU.name?'chatmine':''}">
    <div class="chauth">${m.author}</div>
    <div class="chbub">${m.text}</div>
    <div class="chtime">${new Date(m.ts).toLocaleTimeString('es-AR',{hour:'2-digit',minute:'2-digit'})}</div>
  </div>`).join('');
  el.scrollTop=el.scrollHeight;
}

function updateBadge(){
  const total=Object.values(unreadPrivate).reduce((a,b)=>a+b,0);
  const badge=document.getElementById('chat-badge');
  if(!badge)return;
  if(total>0){badge.style.display='flex';badge.textContent=total;}
  else{badge.style.display='none';}
}

window.sendChat=async()=>{
  const inp=document.getElementById('chat-inp');if(!inp)return;
  const text=inp.value.trim();if(!text||!CU)return;
  await dp('chats/'+chatActiveCid,{author:CU.name,text,ts:Date.now()});
  inp.value='';
};

// Registrar listener de privados al hacer login
function initPrivateListeners(){
  if(!CU||CU.isAdmin)return;
  Object.values(PLAYERS).forEach(p=>{
    if(!p.name||norm(p.name)===norm(CU.name))return;
    const cid='priv_'+[CU.name,p.name].sort().join('_');
    if(!chatListeners[cid]){
      chatListeners[cid]=dl('chats/'+cid,msgs=>{
        CHATS[cid]=msgs||{};
        if(msgs){
          const seen=lastSeenTs[cid]||0;
          const unread=Object.values(msgs).filter(m=>m.ts>seen&&m.author!==CU.name).length;
          unreadPrivate[cid]=unread;
          updateBadge();
          if(chatPanelOpen)buildChatTabs();
        }
      });
    }
  });
}

// ── P1: ACCESO / PERFIL ───────────────────────────────
async function rP1(){
  if(CU&&!CU.isAdmin){await rProfile();initPrivateListeners();updateNav();return;}
  const el=document.getElementById('p1c');
  const rApodo=APODOS[Math.floor(Math.random()*APODOS.length)];
  el.innerHTML=`
    <div class="hero">
      <div class="h-eye">Primera Convocatoria</div>
      <div class="h-title">El Elianato</div>
      <div class="h-roman">MMXXVI</div>
      <div class="h-tag">Intereses Cruzados</div>
    </div>
    <div id="cdbox" class="cdbox"></div>
    <div class="ornament">◆</div>
    <div class="card">
      <div class="cl">Identificación del invitado</div>
      <input class="inp" id="lname" type="text" placeholder="Tu nombre completo" autocomplete="off">
      <div id="pinf" style="display:none;margin-top:9px">
        <div id="pin-label-txt" style="font-size:11px;color:var(--muted);margin-bottom:3px">Elegí un código de hasta 4 dígitos</div>
        <input class="inp pin-inp" id="lpin" type="number" placeholder="0000"
          oninput="if(this.value.length>4)this.value=this.value.slice(0,4)">
        <div id="apodo-wrap" style="margin-top:7px">
          <div style="font-size:11px;color:var(--muted);margin-bottom:3px">Tu apodo sugerido:</div>
          <input class="inp" id="lapodo" value="${rApodo}" placeholder="Apodo mafioso...">
        </div>
      </div>
      <button class="btn bg" onclick="doLogin()">Entrar al evento</button>
      <div id="lmsg" class="msg"></div>
    </div>
    <div class="divrow"><span class="divl"></span><span class="divd">◆</span><span class="divl"></span></div>
    <button class="bgh bsm" style="width:100%" onclick="showAdminModal()">🔐 Acceso organizador</button>`;
  startCD();
  document.getElementById('lname').addEventListener('input',async e=>{
    const name=e.target.value.trim();
    const pf=document.getElementById('pinf');
    const pl=document.getElementById('pin-label-txt');
    if(!name){pf.style.display='none';return;}
    const found=Object.values(PLAYERS).find(p=>norm(p.name)===norm(name));
    pf.style.display='block';
    if(found){
      if(pl)pl.textContent='Ingresá tu código para verificar tu identidad';
      document.getElementById('lapodo').parentElement.style.display='none';
    } else {
      if(pl)pl.textContent='Elegí un código de hasta 4 dígitos';
      const apodoWrap=document.getElementById('lapodo')?.parentElement;
      if(apodoWrap)apodoWrap.style.display='block';
    }
  });
}

window.doLogin=async()=>{
  const name=document.getElementById('lname').value.trim();
  const msg=document.getElementById('lmsg');
  if(!name){msg.innerHTML='<span class="err">Escribí tu nombre.</span>';return;}
  const found=Object.entries(PLAYERS).find(([,p])=>norm(p.name)===norm(name));
  if(found){
    const real=found[1].codigo||'';
    const entered=document.getElementById('lpin')?.value?.trim()||'';
    if(real&&entered!==real){msg.innerHTML='<span class="err">Código incorrecto.</span>';return;}
    msg.innerHTML=`<span style="color:var(--gold)">✓ Bienvenido, ${found[1].name}.</span>`;
    CU={name:found[1].name,isAdmin:false};
  } else {
    const pin=document.getElementById('lpin')?.value?.trim()||'';
    if(!pin||pin.length>4){msg.innerHTML='<span class="err">Elegí un código de hasta 4 dígitos.</span>';return;}
    const apodo=document.getElementById('lapodo')?.value?.trim()||'';
    await dp('players',{name,faccion:'',rol:'',number:'',codigo:pin,apodo,pts:0});
    msg.innerHTML='<span style="color:var(--gold)">✓ Registrado. Nos vemos el 25 de abril.</span>';
    CU={name,isAdmin:false};
  }
  localStorage.setItem('eu',JSON.stringify(CU));
  setTimeout(()=>rP1(),900);
};

async function rProfile(){
  const el=document.getElementById('p1c');
  const me=Object.entries(PLAYERS).find(([,p])=>norm(p.name)===norm(CU.name));
  if(!me){CU=null;localStorage.removeItem('eu');rP1();return;}
  const [myId,myData]=me;
  const myprog=await dg('mysteryProgress/'+myId)||{};
  const mysteries=GS.mysteries||{};
  const myRoleInfo=myData.rol?ROLES_INFO[myData.rol]:null;
  const myPow=await dg('powers/'+myId)||{};
  const powUsed=myPow.used||(myPow.uses||0)>=(myPow.maxUses||1);
  const rawMsgs=await dg('anonMessages/'+myId)||{};
  const msgList=Object.entries(rawMsgs).sort((a,b)=>b[1].ts-a[1].ts);
  // Auto-mark all as read
  const _um=msgList.filter(([,m])=>!m.read);
  if(_um.length)await Promise.all(_um.map(([mid])=>ds('anonMessages/'+myId+'/'+mid+'/read',true)));

  let hits=0,errors=0;
  Object.values(SUBS).filter(s=>s.playerId===myId).forEach(sub=>{
    Object.entries(sub.guesses||{}).forEach(([tid,g])=>{
      const t=PLAYERS[tid];if(!t)return;
      if(g.faccion){if(norm(g.faccion)===norm(t.faccion))hits++;else errors++;}
      if(g.rol){if(norm(g.rol)===norm(t.rol))hits++;else errors++;}
    });
  });
  const posPoints=GS.posPoints||[10,7,5,3,1];
  const pokerPhase=GS.pokerPhase||'A';
  let pokerPts=0;
  Object.values(TABLES).forEach(t=>{
    const pts=t.points||{};const pids=t.players||[];
    if(pokerPhase==='A'){
      const s=[...pids].filter(p=>pts[p]!==undefined).sort((a,b)=>(pts[b]||0)-(pts[a]||0));
      const idx=s.indexOf(myId);if(idx>=0)pokerPts+=(posPoints[idx]||0);
    } else if(pts[myId]!==undefined)pokerPts+=pts[myId];
  });
  const solved=Object.entries(mysteries).filter(([mid])=>myprog[mid]?.solved);
  const facColor=myData.faccion?FC2[myData.faccion]:'var(--gold)';
  const AVATARS=['🤵','🕵️','🔫','💼','🕶️','🥃','🔍','💻','📡','🗝️',
    '⚖️','📰','📋','🖊️','🃏','⭐','💰','🎭','📖','🗡️',
    '🦁','🐺','🦊','🐍','🦅','🦇','🐻','🦈','🐉','🎯',
    '😎','😈','👑','🔥','💎','🧠','⚡','🌙','🎪','🎲',
    '♠','♦','♣','♥','◈','⬡','★','●'];
  const displayAv=myData.avatar||'🎭';

  // Build role card
  let roleCardHTML='';
  // Fallback if role not in ROLES_INFO (old role names)
  if(myData.rol&&!myRoleInfo){
    roleCardHTML='<div class="role-card"><div class="role-priv-lbl">🔒 Tu rol — solo vos lo ves</div>'
      +'<div class="role-nm">'+myData.rol+'</div>'
      +'<div class="role-fc">'+( myData.faccion||'')+'</div>'
      +'<div class="role-ds">Habilidad no disponible para este rol.</div></div>';
  } else if(myRoleInfo){
    roleCardHTML=`<div class="role-card">
      <div class="role-priv-lbl">🔒 Tu rol — solo vos lo ves</div>
      <div class="role-nm">${myData.rol}</div>
      <div class="role-fc" style="color:${FC2[myRoleInfo.fac]||'var(--gold)'}">${FI[myRoleInfo.fac]||''} ${myRoleInfo.fac}</div>
      <div class="role-ds">${myRoleInfo.desc}</div>
      <button class="pwbtn ${powUsed?'used':''}" onclick="activatePower('${myId}','${myData.rol.replace(/'/g,"\\'")}')">
        <div class="pw-nm">⚡ ${myRoleInfo.poder}</div>
        <div class="pw-st">${myRoleInfo.tipo==='Reserva'?'Sin habilidad':myData.rol==='El Fantasma'?'Pasivo — siempre activo':powUsed?'Poder utilizado':'Disponible — tocá para usar'}</div>
      </button>
    </div>`;
  }

  // Build messages
  let msgsHTML='';
  if(msgList.length>0){
    msgsHTML=`<div class="card"><div class="cl">Mensajes del sistema</div>
      ${msgList.map(([mid,m])=>`<div class="amsg ${m.isFalse?'afalse':''}">
        <div class="amsg-tx">${m.text}</div>
        ${m.isFalse?'<div class="amsg-fa">⚠️ Esta pista podría ser falsa</div>':''}
      </div>`).join('')}
    </div>`;
  }

  // Build avatar picker
  const savedBg=myData.profileBg||'default';
  const bgColors=['default','#1a0508','#060814','#061410','#111214','#140f04','#100618'];
  const bgLabels=['Facción','Sangre','Abismo','Jade','Carbón','Bronce','Violeta'];
  const avatarHTML=`<div style="margin-bottom:12px">
    <div style="display:flex;align-items:center;gap:10px;margin-bottom:6px">
      <div style="font-size:36px;width:52px;height:52px;border-radius:12px;display:flex;align-items:center;justify-content:center;background:${facColor}18;border:2px solid ${facColor}44;flex-shrink:0">${displayAv}</div>
      <div style="flex:1">
        <div style="font-size:10px;color:var(--muted);font-family:Cinzel,serif;letter-spacing:.1em;margin-bottom:3px">Avatar y personalización</div>
        <button onclick="(function(){const g=document.getElementById('av-panel');g.style.display=g.style.display==='none'?'block':'none'})()" style="background:none;border:1px solid var(--border);color:var(--gold);font-size:11px;cursor:pointer;font-family:Cinzel,serif;padding:3px 9px;border-radius:4px">Personalizar ▾</button>
      </div>
    </div>
    <div id="av-panel" style="display:none;background:var(--card2);border:1px solid var(--border);border-radius:8px;padding:10px">
      <div style="font-size:9px;color:var(--muted);font-family:Cinzel,serif;letter-spacing:.15em;margin-bottom:6px">AVATAR</div>
      <div style="display:flex;gap:4px;flex-wrap:wrap;margin-bottom:10px">
        ${AVATARS.map(em=>`<button onclick="window.setAvatar('${myId}','${em}')" style="font-size:18px;width:32px;height:32px;background:${em===displayAv?'rgba(201,168,76,.2)':'var(--bg2)'};border:1px solid ${em===displayAv?'var(--gold)':'var(--border)'};border-radius:6px;cursor:pointer">${em}</button>`).join('')}
      </div>
      <div style="font-size:9px;color:var(--muted);font-family:Cinzel,serif;letter-spacing:.15em;margin-bottom:6px">COLOR DE FONDO</div>
      <div style="display:flex;gap:7px;flex-wrap:wrap;margin-bottom:8px">
        ${bgColors.map((c,i)=>`<button onclick="window.setProfileBg('${myId}','${c}')" title="${bgLabels[i]}" style="width:24px;height:24px;border-radius:50%;cursor:pointer;border:2px solid ${c===savedBg?'var(--gold)':'transparent'};background:${c==='default'?facColor:c};position:relative">${c==='default'?'<span style="font-size:8px;color:#fff;position:absolute;inset:0;display:flex;align-items:center;justify-content:center;font-weight:bold">F</span>':''}</button>`).join('')}
      </div>
      <div style="font-size:9px;color:var(--muted);font-family:Cinzel,serif;letter-spacing:.15em;margin-bottom:6px">COLOR DEL NOMBRE</div>
      <div style="display:flex;gap:5px;flex-wrap:wrap">
        ${['#f0e8ff','#c9a84c','#a855f7','#e74c3c','#27ae60','#3498db','#e67e22','#e91e63','#00bcd4','#ff9800'].map(col=>`<button onclick="window.setNameColor('${myId}','${col}')" style="width:22px;height:22px;border-radius:50%;background:${col};border:2px solid ${col===(myData.nameColor||'#f0e8ff')?'#fff':'transparent'};cursor:pointer"></button>`).join('')}
      </div>
    </div>
  </div>`;

  // Compute full-page background
  const pageBg=savedBg==='default'?`${facColor}18`:(savedBg||'transparent');

  el.innerHTML=`
    <div id="p1-profile" style="min-height:100%;background:linear-gradient(180deg,${pageBg} 0%,var(--bg) 50%);padding:18px 14px;margin:-18px -14px;padding-bottom:30px">
    <div class="phead" style="flex-direction:column;align-items:flex-start;gap:10px;padding:16px;background:${facColor}18;border-color:${facColor}44;position:relative;overflow:hidden">
      <div style="position:absolute;top:-30px;right:-30px;width:120px;height:120px;border-radius:50%;background:${facColor}08;pointer-events:none"></div>
      <div style="display:flex;align-items:center;gap:12px;width:100%">
        <div style="font-size:36px;width:52px;height:52px;border-radius:12px;display:flex;align-items:center;justify-content:center;background:${facColor}22;border:2px solid ${facColor}55;flex-shrink:0">${displayAv}</div>
        <div style="flex:1">
          <div style="font-family:Cinzel,serif;font-size:19px;color:${myData.nameColor||'var(--gold)'};font-weight:600;line-height:1.1">${myData.name}</div>
          ${myData.apodo?`<div style="font-family:Cinzel,serif;font-size:13px;color:var(--soft);font-style:italic">"${myData.apodo}"</div>`:''}
          ${myData.faccion?`<div style="color:${facColor};font-size:11px;margin-top:2px">${FI[myData.faccion]} ${myData.faccion}</div>`:''}
        </div>
        <button class="bico" onclick="logout()" title="Salir"><svg style="width:18px;height:18px;stroke:currentColor;fill:none;stroke-width:2" viewBox="0 0 24 24"><path d="M9 21H5a2 2 0 01-2-2V5a2 2 0 012-2h4M16 17l5-5-5-5M21 12H9" stroke-linecap="round" stroke-linejoin="round"/></svg></button>
      </div>
      ${myData.bio?`<div style="font-size:13px;color:var(--soft);font-style:italic;line-height:1.5;border-top:1px solid ${facColor}33;padding-top:9px;width:100%">"${myData.bio}"</div>`:''}
    </div>

    <div class="pstats">
      <div class="psbox"><div class="psval">${hits}</div><div class="pslbl">Aciertos</div></div>
      <div class="psbox"><div class="psval">${errors}</div><div class="pslbl">Errores</div></div>
      <div class="psbox"><div class="psval">${pokerPts}</div><div class="pslbl">Póker</div></div>
      <div class="psbox"><div class="psval">${solved.length}</div><div class="pslbl">Misterios</div></div>
    </div>

    ${roleCardHTML}
    ${msgsHTML}

    <div class="card" style="margin-top:12px">
      <div class="cl">Mi perfil</div>
      ${avatarHTML}
      <div class="pfields">
        <div class="pfrow"><span class="pflbl">Nombre completo</span>
          <input class="inp insm" id="pf-nombre" value="${myData.nombreCompleto||''}" placeholder="—"></div>
        <div class="pfrow"><span class="pflbl">Apodo</span>
          <input class="inp insm" id="pf-apodo" value="${myData.apodo||''}" placeholder="El Zurdo..."></div>
        <div class="pfrow"><span class="pflbl">Edad</span>
          <input class="inp insm" id="pf-edad" type="number" value="${myData.edad||''}" placeholder="—" style="width:65px"></div>
        <div class="pfrow"><span class="pflbl">Estado civil</span>
          <select class="inp insm" id="pf-civil">
            <option value="">—</option>
            ${['Soltero/a','En pareja','Casado/a','Complicado'].map(o=>`<option ${myData.civil===o?'selected':''}>${o}</option>`).join('')}
          </select></div>
        <div class="pfrow" style="flex-direction:column;align-items:flex-start">
          <span class="pflbl" style="margin-bottom:5px">Biografía</span>
          <textarea class="inp" id="pf-bio" rows="3" placeholder="Contá algo de vos...">${myData.bio||''}</textarea>
        </div>
      </div>
      <button class="btn bg" onclick="window.saveProfile('${myId}')">Guardar perfil</button>
    </div>

    ${solved.length>0?`<div class="card"><div class="cl">Misterios resueltos</div>
      ${solved.map(([,m])=>`<div style="display:flex;justify-content:space-between;padding:5px 0;border-bottom:1px solid var(--border);font-size:13px"><span>✅ ${m.titulo||'Misterio'}</span><span style="color:var(--muted)">${(m.phases||[]).length} fases</span></div>`).join('')}
    </div>`:''}

    <div class="divider-row"><span class="divider-line"></span><span class="divider-diamond">◆</span><span class="divider-line"></span></div>
    <button class="btn btn-ghost btn-sm" style="width:100%;opacity:.5" onclick="showAdminModal()">🔐 Acceso organizador</button>
    </div>
  `;
}

window.setAvatar=async(id,em)=>{await du('players/'+id,{avatar:em});rProfile();};
window.setProfileBg=async(id,bg)=>{await du('players/'+id,{profileBg:bg});rProfile();};
window.setNameColor=async(id,color)=>{await du('players/'+id,{nameColor:color});rProfile();};
window.saveProfile=async(id)=>{
  await du('players/'+id,{
    nombreCompleto:document.getElementById('pf-nombre').value.trim(),
    apodo:document.getElementById('pf-apodo').value.trim(),
    edad:document.getElementById('pf-edad').value.trim(),
    civil:document.getElementById('pf-civil').value,
    bio:document.getElementById('pf-bio').value.trim(),
  });
  alert('✓ Perfil guardado.');
  rProfile();
};
window.logout=()=>{CU=null;localStorage.removeItem('eu');chatListeners={};unreadPrivate={};updateNav();rP1();};

function startCD(){
  const target=new Date('2026-04-25T19:30:00');
  function tick(){
    const box=document.getElementById('cdbox');if(!box)return;
    const diff=target-new Date();
    if(diff<=0){box.innerHTML='<div class="cdtitle">¡Esta noche es la noche!</div>';return;}
    const d=Math.floor(diff/86400000),h=Math.floor((diff%86400000)/3600000),
          m=Math.floor((diff%3600000)/60000),s=Math.floor((diff%60000)/1000);
    box.innerHTML=`<div class="cdtitle">Cuenta regresiva al evento</div>
      <div class="cdgrid">
        <div class="cdu"><span class="cdv">${d}</span><span class="cdl">días</span></div>
        <div class="cdu"><span class="cdv">${String(h).padStart(2,'0')}</span><span class="cdl">hs</span></div>
        <div class="cdu"><span class="cdv">${String(m).padStart(2,'0')}</span><span class="cdl">min</span></div>
        <div class="cdu"><span class="cdv">${String(s).padStart(2,'0')}</span><span class="cdl">seg</span></div>
      </div>`;
  }
  tick();setInterval(tick,1000);
}

// ── P2: JUEGO ─────────────────────────────────────────
let myMysteryView=null; // null=lista, mid=detalle

function rP2(){
  const el=document.getElementById('p2c');
  if(!isOn('p2')){el.innerHTML=locked('El juego se habilitará durante el evento');return;}
  const phase=GS.phase||'none';
  if(phase==='C'){rPhaseC();return;}
  const entries=Object.entries(PLAYERS);

  const scores={};const facPts={'La Familia':0,'Agencia':0,'El Concejo':0,'Los Únicos':0};
  entries.forEach(([id,p])=>{scores[id]={name:p.name,faccion:p.faccion,nameColor:p.nameColor||'',pts:0};});
  Object.values(SUBS).forEach(sub=>{
    const pl=PLAYERS[sub.playerId];if(!pl)return;
    let tot=0;
    Object.entries(sub.guesses||{}).forEach(([tid,g])=>{
      const t=PLAYERS[tid];if(!t)return;
      if(g.faccion)tot+=norm(g.faccion)===norm(t.faccion)?getPTS().fA:getPTS().fF;
      if(g.rol)tot+=norm(g.rol)===norm(t.rol)?getPTS().rA:getPTS().rF;
    });
    if(scores[sub.playerId]){
      scores[sub.playerId].pts+=tot;
      const _fk2={'Mafia':'La Familia','Agencia':'Agencia','Municipales':'El Concejo','Especial':'Los Únicos'};const _fkn=_fk2[pl.faccion]||pl.faccion;if(facPts[_fkn]!==undefined)facPts[_fkn]+=tot;
    }
  });
  const ranked=Object.values(scores).sort((a,b)=>b.pts-a.pts);
  const fracRk=Object.entries(facPts).sort((a,b)=>b[1]-a[1]);

  let myId='';let myClues=[];
  const mysteries=GS.mysteries||{};
  if(CU&&!CU.isAdmin){
    const me=entries.find(([,p])=>norm(p.name)===norm(CU.name));
    if(me){myId=me[0];const storedClues=window._myClues||{};myClues=storedClues[myId]||[];}
  }

  el.innerHTML=`
    <div class="phdr">
      <div class="ptitle">🕵️ El Juego</div>
      ${phase!=='none'?`<div class="pbadge b${phase}">Fase ${phase}</div>`:''}
    </div>
    <div class="sgrid">
      <div class="sp"><div class="spt">Individual</div>
        ${ranked.map((p,i)=>`<div class="sr"><span class="rn rn${i+1}">${i+1}</span>
          <span class="sname" style="color:${p.nameColor||''}">${p.name}</span><span class="spts">${p.pts.toFixed(1)}</span></div>`).join('')}
      </div>
      <div class="sp"><div class="spt">Facciones</div>
        ${fracRk.map(([f,pts])=>`<div class="sr"><span style="font-size:14px">${FI[f]}</span>
          <span class="sname" style="color:${FC2[f]}">${f}</span><span class="spts">${pts.toFixed(1)}</span></div>`).join('')}
      </div>
    </div>
    <div class="sec">Jugadores</div>
    <div class="pgrid">
      ${entries.map(([id,p])=>`<div class="pchip" onclick="viewPlayer('${id}')" style="cursor:pointer">
        <span class="cnum">#${p.number||'?'}</span>
        <span class="cname">${p.name}</span>
        ${(()=>{
          const _gfc=CU&&!CU.isAdmin&&myId?Object.values(SUBS).some(s=>s.playerId===myId&&s.guesses&&s.guesses[id]&&s.guesses[id].faccionOk):false;
          if(!p.faccion) return '';
          if(CU&&CU.isAdmin||_gfc) return `<span style="font-size:11px;border:1px solid ${FC2[p.faccion]};border-radius:4px;padding:1px 4px;color:${FC2[p.faccion]};background:${FC2[p.faccion]}22">${FI[p.faccion]}</span>`;
          return '<span style="font-size:11px;color:var(--muted)">❓</span>';
        })()}
      </div>`).join('')}
    </div>
    ${CU&&!CU.isAdmin?`<button class="report-btn" onclick="showComplaint()">⚠️ Queja/sugerencia</button>`:''}
    ${(phase==='A'||phase==='B')&&CU&&!CU.isAdmin?`
      <div class="sec">Mis Pistas</div>
      <div id="clue-section">${buildClueBox(entries,myClues,GS.roles||[])}</div>`:''}
    <div class="sec">Sospechas</div>
    ${buildGuesses(entries,phase,myClues,myId)}
    ${Object.keys(mysteries).length>0&&(phase==='A'||phase==='B')?`
      <div class="sec">Misterios</div>
      <div id="mystery-section"><div class="ibox">Cargando misterios...</div></div>`:''}
    <div class="sec">Glosario</div><button onclick="window.showRolesGlossary()" style="width:100%;background:var(--gp);border:1px solid var(--b2);border-radius:8px;padding:10px 14px;color:var(--gold);font-family:Cinzel,serif;font-size:11px;letter-spacing:.1em;cursor:pointer;text-align:left">📖 Todos los roles y sus habilidades ›</button>
    ${GS.rules?`<div class="sec">Reglas</div><div style="font-size:14px;color:var(--soft);line-height:1.8;background:var(--card2);border:1px solid var(--border);border-radius:8px;padding:13px">${GS.rules.replace(/\n/g,'<br>')}</div>`:''}`;

  document.getElementById('guess-form')?.addEventListener('submit',e=>{e.preventDefault();doSubmit(entries,phase);});
  document.getElementById('clue-form')?.addEventListener('submit',e=>{e.preventDefault();saveClue(entries);});

  // Cargar pistas y misterios async sin bloquear el render
  if(myId){
    dg('clues/'+myId).then(cl=>{
      if(!window._myClues)window._myClues={};
      window._myClues[myId]=cl||[];
      myClues=cl||[];
      const cs=document.getElementById('clue-section');
      if(cs)cs.innerHTML=buildClueBox(entries,myClues,GS.roles||[]);
      document.getElementById('clue-form')?.addEventListener('submit',e=>{e.preventDefault();saveClue(entries);});
    });
  }
  if(Object.keys(mysteries).length>0&&(phase==='A'||phase==='B')&&myId){
    dg('mysteryProgress/'+myId).then(prog=>{
      const ms=document.getElementById('mystery-section');
      if(ms)ms.innerHTML=buildMysteryList(mysteries,prog||{},myId);
    });
  }
}

// ── MISTERIOS ─────────────────────────────────────────
function buildMysteryList(mysteries,progress,myId){
  const entries=Object.entries(mysteries);
  if(!entries.length)return'<div class="ibox">No hay misterios activos.</div>';
  return`<div class="mylist">${entries.map(([mid,m])=>{
    const prog=progress[mid]||{currentPhase:0,solved:false};
    const solved=prog.solved;
    const phases=m.phases||[];
    // contar quién lo resolvió
    const allPlayers=Object.values(PLAYERS);
    // No tenemos progreso de todos — solo mostramos si hay datos en GS
    return`<div class="mycard ${solved?'mysolved':''}" onclick="openMystery('${mid}','${myId}')">
      <div class="mycard-head">
        <span class="mycard-icon">${solved?'✅':'🔍'}</span>
        <div class="mycard-info">
          <div class="mycard-title">${m.titulo||'Misterio'}</div>
          <div class="mycard-meta">${phases.length} ${phases.length===1?'fase':'fases'} · ${solved?'<span style="color:#27ae60">Resuelto</span>':prog.locked?'<span style="color:var(--red)">Bloqueado ❌</span>':'Fase '+(prog.currentPhase+1)+' de '+phases.length}</div>
        </div>
        <span class="mycard-arrow">›</span>
      </div>
    </div>`;
  }).join('')}</div>`;
}

window.openMystery=async(mid,myId)=>{
  const mysteries=GS.mysteries||{};
  const m=mysteries[mid];if(!m)return;
  const prog=await dg('mysteryProgress/'+myId+'/'+mid)||{currentPhase:0,solved:false};
  const ms=document.getElementById('mystery-section');
  if(!ms)return;
  const phases=m.phases||[];
  const ci=prog.currentPhase||0;
  const solved=prog.solved;
  const cp=phases[ci];

  ms.innerHTML=`
    <div class="mydetail">
      <div class="mydetail-back" onclick="closeMystery('${myId}')">‹ Volver a misterios</div>
      <div style="font-family:Cinzel,serif;font-size:14px;color:var(--gold);margin-bottom:6px">${m.titulo}</div>
      <div class="mydetail-progress">
        ${phases.map((_,i)=>`<div class="myprog-dot ${i<ci||solved?'done':i===ci&&!solved?'current':''}"></div>`).join('')}
      </div>
      ${solved
        ?`<div class="myrev">🎯 <strong>Revelación:</strong> ${m.revelation||'—'}</div>`
        :cp?`
          <div style="font-size:12px;color:var(--muted);margin-bottom:8px;font-family:Cinzel,serif;letter-spacing:.1em">
            FASE ${ci+1} DE ${phases.length}
          </div>
          <div class="myclue">${cp.pista||''}</div>
          <div style="font-size:12px;color:var(--muted);margin-bottom:8px">Elegí una respuesta:</div>
          <div class="myopts">
            ${(cp.opciones||[]).map((o,i)=>`<button class="myopt" onclick="answerMys('${myId}','${mid}',${ci},${i},'${myId}')">${o.texto}</button>`).join('')}
          </div>`
        :'<div class="ibox">No hay más fases configuradas.</div>'}
    </div>`;
};

window.closeMystery=async(myId)=>{
  const mysteries=GS.mysteries||{};
  const prog=await dg('mysteryProgress/'+myId)||{};
  const ms=document.getElementById('mystery-section');
  if(ms)ms.innerHTML=buildMysteryList(mysteries,prog,myId);
};

window.answerMys=async(myId,mid,phaseIdx,optIdx)=>{
  const m=(GS.mysteries||{})[mid];if(!m)return;
  const phase=(m.phases||[])[phaseIdx];if(!phase)return;
  const opt=(phase.opciones||[])[optIdx];if(!opt)return;
  const prog=await dg('mysteryProgress/'+myId+'/'+mid)||{currentPhase:0,solved:false};
  if(opt.correcta){
    const next=phaseIdx+1;
    const done=next>=(m.phases||[]).length;
    await ds('mysteryProgress/'+myId+'/'+mid,{currentPhase:next,solved:done,locked:false});
    if(done){
      // Re-render con revelación
      await openMystery(mid,myId);
      // Pequeña animación de celebración
      setTimeout(()=>alert('🎉 ¡Misterio resuelto!\n\n🎯 Revelación: '+(m.revelation||'—')),100);
    } else {
      await openMystery(mid,myId);
      // Feedback visual sin alert para no interrumpir
      const ms=document.getElementById('mystery-section');
      if(ms){
        const banner=document.createElement('div');
        banner.style.cssText='background:rgba(39,174,96,.15);border:1px solid rgba(39,174,96,.4);border-radius:6px;padding:8px 12px;font-size:13px;color:#27ae60;margin-bottom:8px;text-align:center;animation:fadeUp .3s ease';
        banner.textContent='✓ Correcto. Siguiente pista desbloqueada.';
        ms.insertBefore(banner,ms.firstChild);
        setTimeout(()=>banner.remove(),2500);
      }
    }
  } else {
    // Lock the mystery for this player after wrong answer
    await ds('mysteryProgress/'+myId+'/'+mid,{
      currentPhase:prog.currentPhase||0, solved:false, locked:true, lockedAt:Date.now()
    });
    const btn=document.querySelectorAll('.myopt')[optIdx];
    if(btn){btn.style.background='rgba(155,28,58,.15)';btn.style.borderColor='var(--red)';
      setTimeout(()=>{btn.style.background='';btn.style.borderColor='';},600);}
    setTimeout(()=>alert('❌ Respuesta incorrecta. Este misterio quedó bloqueado para vos. Solo otro jugador con el poder adecuado puede desbloquearlo.'),300);
    setTimeout(()=>closeMystery(myId),800);
  }
};

// ── FASE C: REVELACIÓN ────────────────────────────────
function rPhaseC(){
  const el=document.getElementById('p2c');
  const entries=Object.entries(PLAYERS);
  const revIdx=GS.revealIdx||0;
  const byFac={};FACS.forEach(f=>{byFac[f]=[];});
  entries.forEach(([,p])=>{if(p.faccion&&byFac[p.faccion])byFac[p.faccion].push(p);});
  const flat=[];FACS.forEach(f=>byFac[f].forEach(p=>flat.push(p)));
  const revealed=flat.slice(0,revIdx);
  el.innerHTML=`
    <div class="phdr"><div class="ptitle">🎭 Revelación Final</div><div class="pbadge bC">Fase C</div></div>
    <div style="text-align:center;color:var(--muted);font-size:13px;font-style:italic;margin-bottom:14px">El organizador va revelando los roles de a uno...</div>
    ${FACS.map(f=>{
      const group=revealed.filter(p=>p.faccion===f);if(!group.length)return'';
      return`<div style="margin-bottom:16px">
        <div style="font-family:Cinzel,serif;font-size:11px;color:${FC2[f]};letter-spacing:.2em;margin-bottom:7px">${FI[f]} ${f.toUpperCase()}</div>
        ${group.map(p=>`<div class="revcard" style="border-color:${FC2[p.faccion]}44">
          <div class="revnum">#${p.number||'?'}</div>
          <div><div class="revname">${p.name}${p.apodo?` <span style="color:var(--muted);font-size:12px">"${p.apodo}"</span>`:''}</div>
            <div class="revrole" style="color:${FC2[p.faccion]}">${p.rol||'—'}</div></div>
        </div>`).join('')}
      </div>`;
    }).join('')}
    ${revIdx<flat.length?`<div style="text-align:center;color:var(--muted);font-size:13px;margin-top:8px">${flat.length-revIdx} por revelar...</div>`
      :'<div class="ibox iok" style="margin-top:12px">✓ Todos los roles revelados</div>'}`;
}

// ── CLUES ─────────────────────────────────────────────
function buildClueBox(entries,myClues,roles){
  const others=entries.filter(([,p])=>CU&&norm(p.name)!==norm(CU.name));
  const grouped={};
  roles.forEach(r=>{const f=r.faccion||'—';if(!grouped[f])grouped[f]=[];grouped[f].push(r.nombre||r);});
  const clueText=c=>{
    const p=entries.find(([id])=>id===c.playerId);
    const name=p?`#${p[1].number||'?'} ${p[1].name}`:'?';
    if(c.type==='faccion_es')return`${name} → ES de ${c.value}`;
    if(c.type==='faccion_no')return`${name} → NO es de ${c.value}`;
    if(c.type==='rol_es')return`${name} → ES "${c.value}"`;
    if(c.type==='rol_no')return`${name} → NO es "${c.value}"`;
    return'';
  };
  return`<div class="clue-box">
    <div class="clue-title">Registrá tus pistas</div>
    <form id="clue-form" style="margin-top:7px">
      <div style="display:flex;gap:6px;flex-wrap:wrap;margin-bottom:6px">
        <select class="inp insm" id="cl-player" style="flex:1;min-width:100px">
          <option value="">— Jugador —</option>
          ${others.map(([id,p])=>`<option value="${id}">#${p.number||'?'} ${p.name}</option>`).join('')}
        </select>
        <select class="inp insm" id="cl-type" style="flex:1;min-width:100px" onchange="updateClueVal()">
          <option value="">— Tipo —</option>
          <option value="faccion_es">Es de facción</option>
          <option value="faccion_no">NO es de facción</option>
          <option value="rol_es">Es el rol</option>
          <option value="rol_no">NO es el rol</option>
        </select>
      </div>
      <div id="cl-val" style="margin-bottom:6px"></div>
      <button class="btn bg bsm" type="submit" style="width:100%">Guardar pista</button>
    </form>
    ${myClues.length>0?`<div style="margin-top:9px">${myClues.map((c,i)=>`<div class="clue-item">
      <span>${clueText(c)}</span><button class="bico" onclick="delClue(${i})">✕</button>
    </div>`).join('')}</div>`:''}
  </div>`;
}

window.updateClueVal=()=>{
  const type=document.getElementById('cl-type')?.value;
  const wrap=document.getElementById('cl-val');if(!wrap||!type){if(wrap)wrap.innerHTML='';return;}
  const roles=GS.roles||[];
  const grouped={};roles.forEach(r=>{const f=r.faccion||'—';if(!grouped[f])grouped[f]=[];grouped[f].push(r.nombre||r);});
  if(type.startsWith('faccion')){
    wrap.innerHTML=`<select class="inp insm" id="cl-value"><option value="">— Facción —</option>
      ${FACS.map(f=>`<option value="${f}">${FI[f]} ${f}</option>`).join('')}</select>`;
  } else {
    wrap.innerHTML=`<select class="inp insm" id="cl-value"><option value="">— Rol —</option>
      ${Object.entries(grouped).map(([f,rs])=>`<optgroup label="${FI[f]||''} ${f}">
        ${rs.map(r=>`<option value="${r}">${r}</option>`).join('')}</optgroup>`).join('')}</select>`;
  }
};

window.saveClue=async(entries)=>{
  const pid=document.getElementById('cl-player')?.value;
  const type=document.getElementById('cl-type')?.value;
  const val=document.getElementById('cl-value')?.value;
  if(!pid||!type||!val){alert('Completá todos los campos.');return;}
  const me=entries.find(([,p])=>norm(p.name)===norm(CU.name));if(!me)return;
  const _blk=await dg('blocks/'+me[0]);if(_blk&&_blk.until>Date.now()){alert('⚡ El sistema está procesando tu solicitud. Intentá en unos minutos.');return;}
  const [myId]=me;
  const cur=await dg('clues/'+myId)||[];
  cur.push({playerId:pid,type,value:val});
  await ds('clues/'+myId,cur);
  if(!window._myClues)window._myClues={};
  window._myClues[myId]=cur;
  rP2();
};
window.delClue=async i=>{
  const me=Object.entries(PLAYERS).find(([,p])=>norm(p.name)===norm(CU.name));if(!me)return;
  const [myId]=me;
  const cur=await dg('clues/'+myId)||[];
  cur.splice(i,1);
  await ds('clues/'+myId,cur);
  if(!window._myClues)window._myClues={};
  window._myClues[myId]=cur;
  rP2();
};

// ── GUESSES ───────────────────────────────────────────
function buildGuesses(entries,phase,myClues,myId){
  if(phase==='none')return`<div class="ibox">⏳ Las fases aún no comenzaron.</div>`;
  if(phase==='closed')return`<div class="ibox iok">✓ Fase cerrada. Los resultados están arriba.</div>`;
  if(!CU||CU.isAdmin)return`<div class="ibox">Iniciá sesión para participar.</div>`;
  if(!myId)return`<div class="ibox">Tu nombre no está en la lista aún.</div>`;
  const sent=Object.values(SUBS).find(s=>s.playerId===myId&&s.phase===phase);
  if(sent)return`<div class="succ"><div class="succ-i">✓</div>
    <div class="succ-t">Fase ${phase} enviada</div>
    <div style="color:var(--muted);font-size:13px">Puntos: <strong style="color:var(--text)">${sent.total?.toFixed(1)||0}</strong></div></div>`;
  let phaseAHits={};
  if(phase==='B'){const subA=Object.values(SUBS).find(s=>s.playerId===myId&&s.phase==='A');if(subA)phaseAHits=subA.guesses||{};}
  const others=entries.filter(([id])=>id!==myId);
  const roles=GS.roles||[];
  const getCS=tid=>{
    const pc=myClues.filter(c=>c.playerId===tid);
    return{facEs:pc.filter(c=>c.type==='faccion_es').map(c=>c.value),
      facNo:pc.filter(c=>c.type==='faccion_no').map(c=>c.value),
      rolEs:pc.filter(c=>c.type==='rol_es').map(c=>c.value),
      rolNo:pc.filter(c=>c.type==='rol_no').map(c=>c.value)};
  };
  return`<div class="pinfo">${phase==='A'?'Elegí la facción de cada jugador.':'Completá facción y rol. Los verdes ya los acertaste en Fase A.'}</div>
    <form id="guess-form">
      ${others.map(([tid,tp])=>{
        const hitA=phaseAHits[tid];const facOkA=hitA?.faccionOk;const cs=getCS(tid);
        const facHTML=FACS.map(f=>{const ok=cs.facEs.includes(f),no=cs.facNo.includes(f);
          return`<label class="fo ${ok?'fok':no?'fno':''}"><input type="radio" name="fac_${tid}" value="${f}" style="display:none" ${ok?'checked':''}>${FI[f]} ${f} ${ok?'✓':no?'✗':''}</label>`;
        }).join('')+`<label class="fo fem"><input type="radio" name="fac_${tid}" value="" style="display:none">— Sin dato</label>`;
        let rolesDisp=roles;
        if(cs.facEs.length>0)rolesDisp=roles.filter(r=>cs.facEs.includes(r.faccion||''));
        else if(cs.facNo.length>0)rolesDisp=roles.filter(r=>!cs.facNo.includes(r.faccion||''));
        return`<div class="gc ${facOkA?'gg':''}">
          <div class="ghead"><span class="gnum">#${tp.number||'?'}</span><span class="gname">${tp.name}</span>${facOkA?`<span class="gobadge">✓ ${hitA.faccion}</span>`:''}</div>
          ${facOkA?`<input type="hidden" name="fac_${tid}" value="${hitA.faccion}">`:`<div class="fopts">${facHTML}</div>`}
          ${phase==='B'?`<select class="inp" name="rol_${tid}" style="margin-top:6px">
            <option value="">— Rol —</option>
            ${rolesDisp.map(r=>{const n=r.nombre||r;const ok=cs.rolEs.includes(n);const no=cs.rolNo.includes(n);
              return`<option value="${n}" style="color:${ok?'#27ae60':no?'#666':'inherit'};font-weight:${ok?'bold':'normal'}">${ok?'✓ ':no?'✗ ':''}${n}</option>`;}).join('')}
          </select>${cs.rolEs.length>0?`<div style="font-size:11px;color:#27ae60;margin-top:2px">✓ Pista: ${cs.rolEs.join(', ')}</div>`:''}
          ${cs.rolNo.length>0?`<div style="font-size:11px;color:var(--muted);margin-top:1px">✗ Descartados: ${cs.rolNo.join(', ')}</div>`:''}`:''}</div>`;
      }).join('')}
      <button class="btn bg" type="submit" style="margin-top:12px">Confirmar — Fase ${phase}</button>
    </form>`;
}

document.addEventListener('click',e=>{
  const opt=e.target.closest('.fo');if(!opt)return;
  const form=opt.closest('form');if(!form)return;
  const radio=opt.querySelector('input[type="radio"]');
  if(!radio||opt.classList.contains('fno'))return;
  form.querySelectorAll(`input[name="${radio.name}"]`).forEach(r=>r.closest('.fo')?.classList.remove('fsel'));
  radio.checked=true;opt.classList.add('fsel');
});

async function doSubmit(entries,phase){
  const me=entries.find(([,p])=>norm(p.name)===norm(CU.name));if(!me)return;
  const [myId]=me;
  if(Object.values(SUBS).find(s=>s.playerId===myId&&s.phase===phase))return;
  const data=new FormData(document.getElementById('guess-form'));
  const guesses={};let total=0;
  entries.filter(([id])=>id!==myId).forEach(([tid])=>{
    const t=PLAYERS[tid];if(!t)return;
    const f=data.get('fac_'+tid)||'',r=data.get('rol_'+tid)||'';
    const fOk=f&&norm(f)===norm(t.faccion);const rOk=r&&norm(r)===norm(t.rol);
    if(f)total+=fOk?getPTS().fA:getPTS().fF;if(r){const _sf=CU&&PLAYERS[myId]&&t&&PLAYERS[myId].faccion&&t.faccion&&PLAYERS[myId].faccion===t.faccion;total+=rOk?getPTS().rA:(_sf?0:getPTS().rF);}
    guesses[tid]={faccion:f,rol:r,faccionOk:fOk,rolOk:rOk};
  });
  await dp('submissions',{playerId:myId,phase,guesses,total,ts:Date.now()});
  alert('✓ Enviado. Puntos: '+total.toFixed(1));
}


// ── PODERES ───────────────────────────────────────────────────async function _pickPl(prompt_txt){
  const others = Object.entries(PLAYERS).filter(([id])=>CU&&id!==Object.keys(PLAYERS).find(k=>norm(PLAYERS[k].name)===norm(CU.name)));
  const list = others.map(([,p])=>'#'+(p.number||'?')+' '+p.name).join('\n');
  const input = prompt(prompt_txt+'\n\n'+list+'\n\nEscribí el nombre:');
  if(!input) return null;
  const found = others.find(([,p])=>norm(p.name)===norm(input));
  return found ? found[0] : null;
}

window.markAnonRead = async(myId, mid) => {
  await ds('anonMessages/'+myId+'/'+mid+'/read', true);
  rProfile();
};

window.showReport=async()=>{
  const others=Object.values(PLAYERS).filter(p=>p.name&&CU&&norm(p.name)!==norm(CU.name));
  const target=prompt('¿A quién reportás?\n\n'+others.map(p=>`• ${p.name}`).join('\n'));
  if(!target)return;
  const found=others.find(p=>norm(p.name)===norm(target));if(!found){alert('No encontrado.');return;}
  const faccion=prompt(`Facción sospechada de ${found.name}: (Mafia/Agencia/Municipales/Especial)`);
  const motivo=prompt('¿Por qué lo reportás?');if(!motivo)return;
  await dp('reports',{reporter:CU.name,target:found.name,faccion:faccion||'—',motivo,ts:Date.now()});
  alert('✓ Reporte enviado al organizador.');
};

// ── P3: MESAS ─────────────────────────────────────────
const HANDS=[
  {r:1,n:'Escalera Real',d:'A K Q J 10 del mismo palo',ex:'A♠ K♠ Q♠ J♠ 10♠',tag:'Legendaria',tc:'#f59e0b'},
  {r:2,n:'Escalera de Color',d:'5 cartas consecutivas del mismo palo',ex:'7♥ 8♥ 9♥ 10♥ J♥',tag:'Elite',tc:'#8b5cf6'},
  {r:3,n:'Poker',d:'Cuatro cartas del mismo valor',ex:'K♠ K♥ K♦ K♣ 5♦',tag:'Dominante',tc:'#10b981'},
  {r:4,n:'Full House',d:'Trio mas un par',ex:'Q♠ Q♥ Q♦ 8♣ 8♥',tag:'Poderosa',tc:'#ec4899'},
  {r:5,n:'Color',d:'5 cartas del mismo palo (no seguidas)',ex:'2♣ 6♣ 9♣ J♣ A♣',tag:'Fuerte',tc:'#3b82f6'},
  {r:6,n:'Escalera',d:'5 consecutivas de palos mixtos',ex:'5♠ 6♦ 7♥ 8♣ 9♠',tag:'Solida',tc:'#3b82f6'},
  {r:7,n:'Trio',d:'Tres cartas del mismo valor',ex:'J♠ J♥ J♦ 4♣ 9♦',tag:'Decente',tc:'#8b5cf6'},
  {r:8,n:'Doble Pareja',d:'Dos pares distintos',ex:'10♠ 10♦ 4♥ 4♣ K♠',tag:'Comun',tc:'#6366f1'},
  {r:9,n:'Pareja',d:'Dos cartas del mismo valor',ex:'A♠ A♦ 5♥ 7♣ J♠',tag:'Basica',tc:'var(--muted)'},
  {r:10,n:'Carta Alta',d:'Sin combinacion, gana la mas alta',ex:'A♠ K♦ J♥ 7♣ 2♠',tag:'Sin mano',tc:'var(--muted)'},
];
function rP3(){
  const el=document.getElementById('p3c');
  if(!isOn('p3')){el.innerHTML=locked('Las mesas estarán disponibles durante el evento');return;}
  const pokerPhase=GS.pokerPhase||'A';const posPoints=GS.posPoints||[10,7,5,3,1];
  const te=Object.entries(TABLES);
  const ps={};Object.keys(PLAYERS).forEach(pid=>{ps[pid]=0;});
  te.forEach(([,t])=>{
    const pts=t.points||{};const pids=t.players||[];
    if(pokerPhase==='A'){
      const sorted=[...pids].filter(p=>pts[p]!==undefined).sort((a,b)=>(pts[b]||0)-(pts[a]||0));
      sorted.forEach((pid,i)=>{ps[pid]=(ps[pid]||0)+(posPoints[i]||0);});
    } else {pids.forEach(pid=>{if(pts[pid]!==undefined)ps[pid]=(ps[pid]||0)+(pts[pid]||0);});}
  });
  const ranked=Object.entries(ps).map(([pid,p])=>({pid,p,name:PLAYERS[pid]?.name||'?',faccion:PLAYERS[pid]?.faccion||''})).sort((a,b)=>b.p-a.p);
  el.innerHTML=`
    <div class="phdr"><div class="ptitle">🃏 Mesas de Póker</div><div class="pbadge bA">Fase ${pokerPhase}</div></div>
    ${ranked.some(r=>r.p>0)?`<div class="sp" style="margin-bottom:12px">
      <div class="spt">Ranking — Fase ${pokerPhase}</div>
      ${ranked.map((r,i)=>r.p>0?`<div class="sr"><span class="rn rn${i+1}">${i+1}</span>
        <span class="sname">${r.faccion?`<span style="color:${FC2[r.faccion]}">${FI[r.faccion]}</span> `:''}${r.name}</span>
        <span class="spts">${r.p}${pokerPhase==='A'?' pts':' fich'}</span></div>`:'').join('')}
    </div>`:''}
    ${te.length===0?'<div class="ibox">El organizador aún no armó las mesas.</div>'
      :te.map(([,t])=>{
        const pts=t.points||{};
        const sorted=[...(t.players||[])].sort((a,b)=>(pts[b]||0)-(pts[a]||0));
        return`<div class="tcard"><div class="thead">${t.name}</div>
          ${sorted.map((pid,i)=>{const p=PLAYERS[pid];return p?`<div class="trow">
            <div style="display:flex;align-items:center;gap:6px">
              <span class="rn rn${i+1}" style="width:14px">${pts[pid]!==undefined?i+1:'—'}</span>
              ${p.faccion?`<span style="color:${FC2[p.faccion]}">${FI[p.faccion]}</span>`:''}
              <span>${p.name}</span></div>
            <span class="tpts">${pts[pid]!==undefined?pts[pid]+' fichas':'—'}</span>
          </div>`:'';}).join('')}</div>`;
      }).join('')}
    <div class="sec">Reglas del Póker</div>
    <div class="card"><div class="cl">Cómo funciona</div><div style="font-size:13px;color:var(--soft);line-height:1.8"><p style="margin-bottom:6px"><strong style="color:var(--gold)">Fase A — Por posición:</strong> Al cerrar la ronda, los jugadores se ordenan por fichas acumuladas. Cada posición recibe puntos (ej: 1°→10, 2°→7, 3°→5...) configurados por el admin.</p><p style="margin-bottom:6px"><strong style="color:var(--gold)">Fase B — Por fichas:</strong> Las fichas se convierten directamente en puntos de póker.</p><p><strong style="color:var(--gold)">Objetivo:</strong> Acumular la mayor cantidad de fichas en tu mesa para subir en el ranking general.</p></div></div>
    <div class="sec">Ranking de Manos</div>
    <div class="hand-grid">${HANDS.map(h=>`<div class="hand-card hand-r${h.r}"><div style="display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:2px"><div class="hand-rank">#${h.r}</div><div class="hand-badge" style="color:${h.tc};border-color:${h.tc}33;background:${h.tc}11">${h.tag}</div></div><div class="hand-name">${h.n}</div><div class="hand-desc">${h.d}</div><div class="hand-ex">${h.ex}</div></div>`).join('')}</div>`;
}

// ── P4: CATERING ──────────────────────────────────────
function rP4(){
  const el=document.getElementById('p4c');
  const catering=GS.catering||{};
  el.innerHTML=`
    <div class="phdr"><div class="ptitle">🍕 Catering</div></div>
    ${Object.keys(catering).length===0?'<div class="ibox">El menú se publicará pronto.</div>'
      :Object.entries(catering).map(([cat,items])=>`<div class="mcard">
        <div class="mcat">${cat}</div>
        <div class="mitems">${(items||[]).map(i=>`<div class="mitem"><span class="mdot">◆</span>${i}</div>`).join('')}</div>
      </div>`).join('')}`;
}

// ── ADMIN ─────────────────────────────────────────────
async function rAdmin(){
  const el=document.getElementById('admc');
  const complaints=await dg('complaints')||{};
  const complaintsHTML = Object.keys(complaints).length === 0
    ? '<div class="ibox">Sin quejas.</div>'
    : Object.entries(complaints).sort((a,b)=>b[1].ts-a[1].ts).map(([cid,c])=>{
        const time = new Date(c.ts).toLocaleTimeString('es-AR',{hour:'2-digit',minute:'2-digit'});
        return '<div style="padding:7px 0;border-bottom:1px solid var(--border)">'
          +'<strong style="font-size:13px">'+c.from+'</strong>'
          +'<div style="font-size:14px;color:var(--soft);margin-top:3px;line-height:1.5">'+c.msg+'</div>'
          +'<div style="font-size:10px;color:var(--mut);margin-top:3px">'+time+'</div>'
          +'</div>';
      }).join('');

  const entries=Object.entries(PLAYERS);
  const phase=GS.phase||'none';
  const enabled=GS.enabled||{};
  const roles=GS.roles||[];
  const catering=GS.catering||{};
  const rules=GS.rules||'';
  const pokerRules=GS.pokerRules||'';
  const pokerRules=GS.pokerRules||'';
  const rolesTexto=roles.map(r=>typeof r==='object'?`${r.nombre||''}|${r.faccion||''}|${r.numero||''}`:(r||'')).join('\n');

  const adminRank=entries.map(([id,p])=>{
    let pts=0,hits=0;
    Object.values(SUBS).filter(s=>s.playerId===id).forEach(sub=>{
      Object.entries(sub.guesses||{}).forEach(([tid,g])=>{
        const t=PLAYERS[tid];if(!t)return;
        const fOk=g.faccion&&norm(g.faccion)===norm(t.faccion);
        const rOk=g.rol&&norm(g.rol)===norm(t.rol);
        if(g.faccion){pts+=fOk?getPTS().fA:getPTS().fF;if(fOk)hits++;}
        if(g.rol){pts+=rOk?getPTS().rA:getPTS().rF;if(rOk)hits++;}
      });
    });
    return{id,name:p.name,faccion:p.faccion,rol:p.rol,number:p.number,codigo:p.codigo||'—',pts,hits};
  }).sort((a,b)=>b.pts-a.pts);



  el.innerHTML=`
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:16px">
      <div class="atitle">Panel Admin</div>
      <button class="bgh bsm" onclick="adminLogout()">Salir</button>
    </div>

    <div class="acard ${GS.testMode?'acard-on':''}">
      <div class="cl">Modo Prueba</div>
      <button class="btn ${GS.testMode?'bg':'bgh'}" onclick="toggleTest()">${GS.testMode?'🟡 Activo — Desactivar':'⚪ Activar Modo Prueba'}</button>
    </div>

    <div class="acard">
      <div class="cl">Control del Evento</div>
      <div class="ctrlgrid">
        <div>
          <div class="asl">Páginas activas</div>
          ${['p2','p3','p4'].map(p=>`<label class="tglrow">
            <span style="font-size:13px">${p==='p2'?'🕵️ Juego':p==='p3'?'🃏 Mesas':'🍕 Catering'}</span>
            <input type="checkbox" ${enabled[p]?'checked':''} onchange="togglePage('${p}',this.checked)">
          </label>`).join('')}
          <label class="tglrow">
            <span style="font-size:13px">💬 Chat</span>
            <input type="checkbox" ${GS.chatEnabled?'checked':''} onchange="toggleChat(this.checked)">
          </label>
        </div>
        <div>
          <div class="asl">Fase: <strong style="color:var(--gold)">${phase.toUpperCase()}</strong></div>
          ${['A','B','closed','C','none'].map(f=>`<button class="bgh bsm" style="width:100%;margin-bottom:3px" onclick="setPhase('${f}')">
            ${f==='A'?'Fase A':f==='B'?'Fase B':f==='closed'?'Cerrar':f==='C'?'—':'Resetear'}
          </button>`).join('')}
        </div>
      </div>
    </div>

    <div class="acard">
      <div class="cl">Jugadores (${entries.length})</div>
      <button class="bgh bsm" onclick="addPlayer()" style="margin-bottom:9px">+ Agregar</button>
      <div class="ptbl">
        <div class="pthdr"><span>#</span><span>Nombre</span><span>Cód</span><span>Fac · Rol</span><span></span></div>
        ${entries.map(([id,p])=>`<div class="ptrow">
          <span class="ptnum">${p.number||'?'}</span>
          <span style="font-size:13px">${p.name}</span>
          <span class="ptcode">${p.codigo||'—'}</span>
          <span style="font-size:11px;color:${FC2[p.faccion]||'var(--muted)'};">${p.faccion||'—'}·${p.rol||'—'}</span>
          <span class="ptacts">
            <button class="bico" onclick="editPlayer('${id}')">✏️</button>
            <button class="bico" onclick="delPlayer('${id}')">✕</button>
          </span>
        </div>`).join('')}
      </div>
    </div>

    <div class="acard">
      <div class="cl">Asignación de roles</div>
      <p class="ahint">Asigná el número de collar a cada rol. Al guardar, el sistema asigna facción y rol automáticamente a cada jugador.</p>
      ${['La Familia','Agencia','El Concejo','Los Únicos'].map(fac=>{
        const fr=ROLES_PRESET.filter(r=>r.fac===fac);
        const ra=GS.roleAssignments||{};
        return`<div style="margin-bottom:12px">
          <div style="font-family:Cinzel,serif;font-size:10px;letter-spacing:.2em;color:${FC2[fac]||'var(--gold)'};margin-bottom:5px">${FI[fac]||''} ${fac.toUpperCase()}</div>
          ${fr.map(r=>`<div style="display:flex;align-items:center;gap:8px;padding:4px 0;border-bottom:1px solid var(--border)">
            <span style="flex:1;font-size:12px;color:${r.tipo==='Reserva'?'var(--muted)':'var(--soft)'}">${r.nombre}</span>
            <span style="font-size:9px;color:var(--muted);min-width:80px;text-align:right">${r.tipo}</span>
            <input type="number" class="inp insm" style="width:50px;text-align:center" id="ra_${r.nombre.replace(/[^a-zA-Z0-9]/g,'_')}" value="${ra[r.nombre]||''}" placeholder="#" min="1" max="30">
          </div>`).join('')}
        </div>`;
      }).join('')}
      <button class="btn bg" onclick="window.saveRoleAssignments()">Guardar asignaciones</button>
    </div>
    <div class="acard">
      <div class="cl">Resultados detallados</div>
      ${adminRank.map((s,i)=>`<div class="resrow">
        <span class="rn rn${i+1}">${i+1}</span>
        <span style="flex:1;font-size:14px">${s.name} <span style="font-size:11px;color:${FC2[s.faccion]||'var(--muted)'}"> ${s.faccion||''}</span></span>
        <span style="color:var(--gold);font-weight:bold;font-family:Cinzel,serif">${s.pts.toFixed(1)}</span>
      </div>
      <div style="margin-bottom:9px">${Object.values(SUBS).filter(sub=>sub.playerId===s.id).map(sub=>`
        <div class="sublbl">Fase ${sub.phase}:</div>
        ${Object.entries(sub.guesses||{}).map(([tid,g])=>{
          const t=PLAYERS[tid];if(!t)return'';
          const fOk=g.faccion&&norm(g.faccion)===norm(t.faccion);
          const rOk=g.rol&&norm(g.rol)===norm(t.rol);
          return`<div class="subdet"><span class="subtgt">${t.name}:</span>
            ${g.faccion?`<span class="${fOk?'ok':'err'}">${g.faccion}${fOk?'✓':'✗'}</span>`:'<span class="muted">—</span>'}
            ${g.rol?`<span class="${rOk?'ok':'muted'}">${g.rol}${rOk?'✓':''}</span>`:''}
          </div>`;}).join('')}`).join('')}</div>`).join('')}
    </div>

    <div class="acard">
      <div class="cl">Control Póker</div>
      <div class="asl">Fase: <strong style="color:var(--gold)">${GS.pokerPhase||'A'}</strong></div>
      <div style="display:flex;gap:6px;margin:6px 0 10px;flex-wrap:wrap">
        <button class="bgh bsm" onclick="ds('gamestate/pokerPhase','A')">Fase A</button>
        <button class="bgh bsm" onclick="ds('gamestate/pokerPhase','B')">Fase B</button>
      </div>
      <div class="asl">Puntos por posición Fase A (separados por coma):</div>
      <input class="inp" id="ppts" value="${(GS.posPoints||[10,7,5,3,1]).join(',')}" style="max-width:170px">
      <button class="bgh bsm" onclick="savePPts()" style="margin-top:5px">Guardar</button>
    </div>

    <div class="acard">
      <div class="cl">Mesas de Póker</div>
      <div style="display:flex;gap:6px;flex-wrap:wrap;margin-bottom:10px">
        <button class="bgh bsm" onclick="showCT('manual')">+ Manual</button>
        <button class="bgh bsm" onclick="showCT('auto')">🎲 Aleatoria</button>
      </div>
      <div id="ct-panel"></div>
      ${Object.entries(TABLES).map(([tid,t])=>`<div class="tcard" style="margin-bottom:7px">
        <div class="thead" style="display:flex;justify-content:space-between">
          <span>${t.name}</span><button class="bico" onclick="delTable('${tid}')">✕</button>
        </div>
        ${(t.players||[]).map(pid=>{const p=PLAYERS[pid];if(!p)return'';return`<div class="trow">
          <span>${p.name}</span>
          <input type="number" class="inp insm" value="${t.points?.[pid]??''}" placeholder="fichas"
            style="width:65px;text-align:center" onchange="saveTpts('${tid}','${pid}',this.value)">
        </div>`;}).join('')}
      </div>`).join('')||'<div class="ibox">No hay mesas aún.</div>'}
    </div>

    <div class="acard">
      <div class="cl">Misterios</div>
      <button class="bgh bsm" onclick="addMystery()" style="margin-bottom:9px">+ Nuevo misterio</button>
      ${Object.entries(GS.mysteries||{}).map(([mid,m])=>`<div class="acard" style="background:var(--bg2);margin-bottom:6px">
        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:5px">
          <span style="font-family:Cinzel,serif;font-size:13px;color:var(--gold)">${m.titulo}</span>
          <button class="bico" onclick="delMystery('${mid}')">✕</button>
        </div>
        <div style="font-size:11px;color:var(--muted)">${(m.phases||[]).length} fases · Revela: ${m.revelation||'—'}</div>
        <button class="bgh bsm" onclick="editMystery('${mid}')" style="margin-top:5px">✏️ Editar fases</button>
      </div>`).join('')||'<div class="ibox">No hay misterios.</div>'}
    </div>

    <div class="acard">
      <div class="cl">Quejas y sugerencias</div>
      ${complaintsHTML}
    </div>

    <div class="acard">
      <div class="cl">Catering</div>
      <p class="ahint">Formato: <strong style="color:var(--gold)">##Categoría</strong> luego ítems, uno por línea.</p>
      <textarea class="inp" id="cat-ed" rows="10">${cToTxt(catering)}</textarea>
      <button class="btn bg" onclick="saveCat()">Guardar catering</button>
    </div>


    <div class="acard">
      <div class="cl">Puntuación configurable</div>
      <p class="ahint">8 valores para Fase A y B. Regla automática: si alguien de tu misma facción acierta tu rol, no genera penalización.</p>
      <div class="scgrid">
        <div class="scfield"><span class="sclbl">Acertás facción</span><input class="inp insm" id="sc-fA" type="number" step="0.5" value="${(GS.ptsConfig||DEFAULT_PTS).fA}"></div>
        <div class="scfield"><span class="sclbl">Fallás facción</span><input class="inp insm" id="sc-fF" type="number" step="0.5" value="${(GS.ptsConfig||DEFAULT_PTS).fF}"></div>
        <div class="scfield"><span class="sclbl">Otro acierta tu fac.</span><input class="inp insm" id="sc-fOA" type="number" step="0.5" value="${(GS.ptsConfig||DEFAULT_PTS).fOA}"></div>
        <div class="scfield"><span class="sclbl">Otro falla tu fac.</span><input class="inp insm" id="sc-fOF" type="number" step="0.5" value="${(GS.ptsConfig||DEFAULT_PTS).fOF}"></div>
        <div class="scfield"><span class="sclbl">Acertás rol</span><input class="inp insm" id="sc-rA" type="number" step="0.5" value="${(GS.ptsConfig||DEFAULT_PTS).rA}"></div>
        <div class="scfield"><span class="sclbl">Fallás rol</span><input class="inp insm" id="sc-rF" type="number" step="0.5" value="${(GS.ptsConfig||DEFAULT_PTS).rF}"></div>
        <div class="scfield"><span class="sclbl">Otro acierta tu rol</span><input class="inp insm" id="sc-rOA" type="number" step="0.5" value="${(GS.ptsConfig||DEFAULT_PTS).rOA}"></div>
        <div class="scfield"><span class="sclbl">Otro falla tu rol</span><input class="inp insm" id="sc-rOF" type="number" step="0.5" value="${(GS.ptsConfig||DEFAULT_PTS).rOF}"></div>
      </div>
      <div style="margin-top:10px">
        <div class="asl" style="margin-bottom:5px">Multiplicador de fase</div>
        <div style="display:flex;gap:8px;align-items:center;flex-wrap:wrap">
          <select class="inp insm" id="sc-mult-fase" style="flex:1;min-width:80px">
            <option value="">Sin multiplicador</option>
            <option value="A" ${GS.phaseMultiplier?.fase==='A'?'selected':''}>Fase A</option>
            <option value="B" ${GS.phaseMultiplier?.fase==='B'?'selected':''}>Fase B</option>
          </select>
          <input class="inp insm" id="sc-mult-val" type="number" step="0.5" min="1" max="5" style="width:65px"
            value="${GS.phaseMultiplier?.mult||2}" placeholder="x2">
          <span style="font-size:12px;color:var(--muted)">× todos los puntos de esa fase</span>
        </div>
      </div>
      <button class="btn bg" onclick="window.savePtsConfig()" style="margin-top:8px">Guardar puntuación</button>
    </div>
       </div>

    <div class="acard">
      <div class="cl">Banco de pistas</div>
      <p class="ahint">Pistas editables para revelar durante el evento. #N = número de collar, [ROL] y [FACCION] = marcadores.</p>
      ${['comun','pocoComun','rara','especial'].map(tier=>{
        const labels={comun:'Común',pocoComun:'Poco común',rara:'Rara',especial:'Especial'};
        const bank=(GS.clueBank||DEFAULT_CLUES)[tier]||[];
        return`<div style="margin-bottom:10px">
          <div style="font-family:Cinzel,serif;font-size:9px;letter-spacing:.2em;color:var(--pl);margin-bottom:4px">${labels[tier].toUpperCase()} (${bank.length})</div>
          ${bank.map((c,i)=>`<div style="display:flex;align-items:flex-start;gap:5px;padding:3px 0;border-bottom:1px solid var(--border)">
            <span style="flex:1;font-size:11px;color:var(--soft);line-height:1.5">${c}</span>
            <button class="bico" onclick="window.editClue('${tier}',${i})" style="font-size:10px;flex-shrink:0">✏️</button>
            <button class="bico" onclick="window.delClue('${tier}',${i})" style="font-size:10px;flex-shrink:0">✕</button>
          </div>`).join('')}
          <button class="bgh bsm" onclick="window.addClue('${tier}')" style="margin-top:4px;width:100%">+ Agregar pista ${labels[tier].toLowerCase()}</button>
        </div>`;
      }).join('')}
    </div>
    <div class="acard">
      <div class="cl">Reglas del juego</div>
      <p class="ahint">Aparecen al final de la pestaña Juego.</p>
      <textarea class="inp" id="rules-ed" rows="6" placeholder="Escribí las reglas...">${rules}</textarea>
      <button class="btn bg" onclick="window.saveRules2()">Guardar reglas</button>
    </div>
    <div class="acard">
      <div class="cl">Reglas del Póker</div>
      <p class="ahint">Aparecen en la pestaña Mesas. Explicá cómo funciona el póker esta noche.</p>
      <textarea class="inp" id="poker-rules-ed" rows="5" placeholder="Ej: Cada ronda dura 20 minutos...">${pokerRules}</textarea>
      <button class="btn bg" onclick="window.savePokerRules()">Guardar reglas de póker</button>
    </div>

      <div style="margin-bottom:10px">
        <div class="asl">Cambiar PIN</div>
        <input class="inp" id="newpin" type="password" placeholder="Nuevo PIN">
        <button class="bgh bsm" onclick="chPin()" style="margin-top:5px">Cambiar</button>
      </div>
      <button class="bgh bsm" style="width:100%;margin-bottom:6px" onclick="resetSubs()">Resetear envíos</button>
      <button class="bd bsm" style="width:100%" onclick="resetAll()">⚠️ Resetear TODO</button>
    </div>`;
}

// ── ADMIN ACTIONS ─────────────────────────────────────
window.adminLogout=()=>{CU=null;localStorage.removeItem('eu');nav('p1');};
window.toggleTest=()=>ds('gamestate/testMode',!GS.testMode);
window.togglePage=(p,v)=>ds('gamestate/enabled/'+p,v);
window.toggleChat=v=>ds('gamestate/chatEnabled',v);
window.setPhase=phase=>ds('gamestate/phase',phase);
window.savePPts=async()=>{
  const pts=document.getElementById('ppts').value.split(',').map(v=>parseInt(v.trim())).filter(v=>!isNaN(v));
  if(!pts.length){alert('Formato: 10,7,5,3,1');return;}
  await ds('gamestate/posPoints',pts);alert('✓ Puntos guardados.');
};
window.revNext=async()=>{
  const byFac={};FACS.forEach(f=>{byFac[f]=[];});
  Object.values(PLAYERS).forEach(p=>{if(p.faccion&&byFac[p.faccion])byFac[p.faccion].push(p);});
  const flat=[];FACS.forEach(f=>byFac[f].forEach(p=>flat.push(p)));
  const cur=GS.revealIdx||0;if(cur>=flat.length){alert('Ya se revelaron todos.');return;}
  await ds('gamestate/revealIdx',cur+1);
};
window.addPlayer=async()=>{const name=prompt('Nombre:');if(!name)return;await dp('players',{name,faccion:'',rol:'',number:'',codigo:'',pts:0});};
window.editPlayer=async id=>{
  const p=PLAYERS[id];if(!p)return;
  const name=prompt('Nombre:',p.name)??p.name;
  const number=prompt('Número de collar:',p.number)??p.number;
  const codigo=prompt('Código de ingreso:',p.codigo)??p.codigo;
  // Auto-assign faccion+rol from roleAssignments
  let faccion=p.faccion,rol=p.rol;
  if(number){
    const ra=GS.roleAssignments||{};
    const found=Object.entries(ra).find(([,n])=>String(n)===String(number));
    if(found){
      const preset=ROLES_PRESET.find(r=>r.nombre===found[0]);
      if(preset){
        faccion=preset.fac;rol=found[0];
        alert('Rol asignado automáticamente: '+found[0]+' ('+preset.fac+')');
      }
    }
  }
  await du('players/'+id,{name,number,faccion,rol,codigo});
};
window.delPlayer=async id=>{if(!confirm('¿Eliminar?'))return;await dd('players/'+id);};
window.delReport=async id=>{await dd('reports/'+id);rAdmin();};
window.showCT=async mode=>{
  const entries=Object.entries(PLAYERS);
  const panel=document.getElementById('ct-panel');
  if(mode==='auto'){
    panel.innerHTML=`<div class="acard" style="margin-bottom:9px">
      <div class="cl">Mesa aleatoria</div>
      <div class="asl">Jugadores por mesa:</div>
      <input class="inp" id="tsize" type="number" value="5" min="2" style="width:65px">
      <button class="btn bg" onclick="createAuto()" style="margin-top:6px">Generar</button>
    </div>`;
  } else {
    panel.innerHTML=`<div class="acard" style="margin-bottom:9px">
      <div class="cl">Mesa manual</div>
      <input class="inp" id="tname" placeholder="Nombre (ej: Mesa 1)" style="margin-bottom:6px">
      <div style="max-height:190px;overflow-y:auto;border:1px solid var(--border);border-radius:6px;padding:6px;margin-top:4px">
        ${entries.map(([id,p])=>`<label style="display:flex;align-items:center;gap:6px;padding:5px 0;cursor:pointer;font-size:14px">
          <input type="checkbox" value="${id}" class="tpc" style="accent-color:var(--gold)">
          <span class="ptnum">#${p.number||'?'}</span> ${p.name}
        </label>`).join('')}
      </div>
      <button class="btn bg" onclick="createManual()" style="margin-top:7px">Crear mesa</button>
    </div>`;
  }
};
window.createAuto=async()=>{
  const size=parseInt(document.getElementById('tsize').value)||5;
  const allIds=Object.keys(PLAYERS);const shuffled=[...allIds].sort(()=>Math.random()-.5);
  const num=Object.keys(TABLES).length+1;
  for(let i=0;i<shuffled.length;i+=size)await dp('tables',{name:'Mesa '+(num+Math.floor(i/size)),players:shuffled.slice(i,i+size),points:{}});
  document.getElementById('ct-panel').innerHTML='';
};
window.createManual=async()=>{
  const name=document.getElementById('tname').value.trim();
  const pids=Array.from(document.querySelectorAll('.tpc:checked')).map(b=>b.value);
  if(!name||!pids.length){alert('Completá nombre y elegí jugadores.');return;}
  await dp('tables',{name,players:pids,points:{}});
  document.getElementById('ct-panel').innerHTML='';
};
window.saveTpts=async(tid,pid,val)=>ds('tables/'+tid+'/points/'+pid,parseFloat(val)||0);
window.delTable=async tid=>{if(!confirm('¿Eliminar?'))return;await dd('tables/'+tid);};
function cToTxt(c){return Object.entries(c).map(([cat,items])=>`##${cat}\n${(items||[]).join('\n')}`).join('\n\n');}
function txtToC(text){const r={};let cur=null;text.split('\n').forEach(line=>{const t=line.trim();if(!t)return;if(t.startsWith('##')){cur=t.slice(2).trim();r[cur]=[];}else if(cur)r[cur].push(t);});return r;}

window.savePtsConfig = async() => {
  const v = id => parseFloat(document.getElementById(id)?.value);
  const cfg = {
    fA:v('sc-fA')||2, fF:v('sc-fF')||-0.5,
    fOA:v('sc-fOA')||-0.5, fOF:v('sc-fOF')||0.5,
    rA:v('sc-rA')||5, rF:v('sc-rF')||-2,
    rOA:v('sc-rOA')||-1, rOF:v('sc-rOF')||1
  };
  await ds('gamestate/ptsConfig', cfg);
  alert('✓ Puntuación guardada.');
};
window.showComplaint = async() => {
  const msg = prompt('Queja o sugerencia para el organizador:');
  if(!msg) return;
  await dp('complaints', {from:CU.name, msg, ts:Date.now()});
  alert('✓ Enviado al organizador.');
};
window.savePtsConfig=async()=>{
  const v=id=>parseFloat(document.getElementById(id)?.value);
  const cfg={fA:v('sc-fA')||2,fF:v('sc-fF')||-0.5,fOA:v('sc-fOA')||-0.5,fOF:v('sc-fOF')||0.5,
    rA:v('sc-rA')||5,rF:v('sc-rF')||-2,rOA:v('sc-rOA')||-1,rOF:v('sc-rOF')||1};
  await ds('gamestate/ptsConfig',cfg);
  const mFase=document.getElementById('sc-mult-fase')?.value;
  const mVal=parseFloat(document.getElementById('sc-mult-val')?.value)||2;
  if(mFase) await ds('gamestate/phaseMultiplier',{fase:mFase,mult:mVal});
  else await ds('gamestate/phaseMultiplier',null);
  alert('Puntuación guardada.');
};
window.saveRoleAssignments=async()=>{
  const ra={};
  ROLES_PRESET.forEach(r=>{
    const sid=r.nombre.replace(/[^a-zA-Z0-9]/g,'_');
    const inp=document.getElementById('ra_'+sid);
    if(inp&&inp.value.trim())ra[r.nombre]=inp.value.trim();
  });
  await ds('gamestate/roleAssignments',ra);
  // Auto-apply to players
  const entries=Object.entries(PLAYERS);
  for(const [pid,p] of entries){
    if(!p.number)continue;
    const found=Object.entries(ra).find(([,n])=>String(n)===String(p.number));
    if(found){
      const [rolName]=found;
      const preset=ROLES_PRESET.find(r=>r.nombre===rolName);
      if(preset)await du('players/'+pid,{rol:rolName,faccion:preset.fac});
    }
  }
  alert('Asignaciones guardadas y aplicadas a jugadores con número de collar.');
};
window.editClue=async(tier,idx)=>{
  const bank=GS.clueBank||JSON.parse(JSON.stringify(DEFAULT_CLUES));
  const cur=(bank[tier]||[])[idx]||'';
  const newText=prompt('Editar pista:',cur);if(!newText)return;
  if(!bank[tier])bank[tier]=[];
  bank[tier][idx]=newText;
  await ds('gamestate/clueBank',bank);
};
window.addClue=async(tier)=>{
  const text=prompt('Nueva pista (usá #N para número, [ROL] o [FACCION] como marcadores):');if(!text)return;
  const bank=GS.clueBank||JSON.parse(JSON.stringify(DEFAULT_CLUES));
  if(!bank[tier])bank[tier]=[];
  bank[tier].push(text);
  await ds('gamestate/clueBank',bank);
};
window.delClue=async(tier,idx)=>{
  if(!confirm('¿Eliminar esta pista?'))return;
  const bank=GS.clueBank||JSON.parse(JSON.stringify(DEFAULT_CLUES));
  if(bank[tier])bank[tier].splice(idx,1);
  await ds('gamestate/clueBank',bank);
};
window.showRolesGlossary=()=>{
  const TIPOS={Protector:'🛡️',Informante:'🔍',Atacante:'⚔️','Atacante A':'⚔️','Atacante B':'⚔️','Atacante C':'⚔️','Atacante D':'⚔️',Todoterreno:'🔄',Comodín:'🃏',Reserva:'—'};
  const facs=['La Familia','Agencia','El Concejo','Los Únicos'];
  let html='<div style="position:fixed;inset:0;z-index:500;background:rgba(0,0,0,.9);overflow-y:auto;padding:16px">';
  html+='<div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:14px">';
  html+='<div style="font-family:Cinzel,serif;font-size:15px;color:var(--gold)">📖 Todos los roles</div>';
  html+='<button onclick="document.getElementById(\'roles-glossary\').remove()" style="background:none;border:1px solid var(--border);color:var(--muted);font-size:13px;cursor:pointer;padding:4px 10px;border-radius:4px;font-family:Cinzel,serif">✕ Cerrar</button></div>';
  facs.forEach(fac=>{
    const facRoles=Object.entries(ROLES_INFO).filter(([,r])=>r.fac===fac);
    html+='<div style="margin-bottom:16px">';
    html+='<div style="font-family:Cinzel,serif;font-size:10px;letter-spacing:.22em;color:'+(FC2[fac]||'var(--gold)')+';margin-bottom:8px">'+(FI[fac]||'')+' '+fac.toUpperCase()+'</div>';
    facRoles.forEach(([nombre,r])=>{
      html+='<div style="background:var(--card);border:1px solid var(--border);border-radius:8px;padding:10px;margin-bottom:6px">';
      html+='<div style="display:flex;align-items:center;gap:8px;margin-bottom:5px">';
      html+='<span style="font-size:14px">'+(TIPOS[r.tipo]||'●')+'</span>';
      html+='<span style="font-family:Cinzel,serif;font-size:13px;color:var(--gold)">'+(nombre)+'</span>';
      html+='<span style="font-size:9px;color:var(--muted);font-family:Cinzel,serif;letter-spacing:.1em;margin-left:auto">'+r.tipo+'</span></div>';
      if(r.tipo!=='Reserva')html+='<div style="font-size:12px;color:var(--soft);line-height:1.5">'+r.desc+'</div>';
      html+='</div>';
    });
    html+='</div>';
  });
  html+='</div>';
  const overlay=document.createElement('div');overlay.id='roles-glossary';
  overlay.innerHTML=html;document.body.appendChild(overlay);
};
window.showComplaint=async()=>{
  const msg=prompt('Queja o sugerencia para el organizador:');if(!msg)return;
  await dp('complaints',{from:CU.name,msg,ts:Date.now()});alert('Enviado.');
};
window.activatePower=async(myId,rolName)=>{
  const rInfo=ROLES_INFO[rolName];if(!rInfo){alert('Rol no reconocido.');return;}
  const pow=await dg('powers/'+myId)||{};
  const uses=pow.uses||0;const maxU=pow.maxUses||1;
  if(pow.used||(maxU>1&&uses>=maxU)){alert('Ya usaste tu poder esta noche.');return;}
  const _sys=async(toId,text,isFalse)=>{const mid='m'+Date.now()+Math.random().toString(36).slice(2,5);await ds('anonMessages/'+toId+'/'+mid,{text,isFalse:!!isFalse,read:false,ts:Date.now()});};
  const _save=async(extra={})=>{const nu=uses+1;await ds('powers/'+myId,{...pow,...extra,uses:nu,used:nu>=maxU,rol:rolName,ts:Date.now()});};

  // ── PROTECTORES ──────────────────────────────────────────────
  if(rInfo.tipo==='Protector'){
    const others=Object.entries(PLAYERS).filter(([id])=>id!==myId);
    const list=others.map(([,p])=>'#'+(p.number||'?')+' '+p.name).join('\n');
    const input=prompt('¿A quién protegés esta fase?\n(Solo protege contra votos de su misma facción)\n\n'+list+'\n\nEscribí el nombre:');
    if(!input)return;
    const found=others.find(([,p])=>norm(p.name)===norm(input));
    if(!found){alert('Jugador no encontrado.');return;}
    await ds('protections/'+myId,{target:found[0],rol:rolName,ts:Date.now()});
    await ds('powers/'+myId,{used:true,rol:rolName,target:found[0],ts:Date.now()});
    alert('Protección activada sobre '+PLAYERS[found[0]]?.name+'.');
  }

  // ── INFORMANTES ───────────────────────────────────────────────
  else if(rInfo.tipo==='Informante'){
    const accion=prompt('¿Qué querés hacer?\n1 - Ver pistas de un jugador\n2 - Confirmar facción de un número\n3 - Confirmar rol de un jugador');
    if(!accion)return;
    if(accion==='1'){
      const others=Object.entries(PLAYERS).filter(([id])=>id!==myId);
      const list=others.map(([,p])=>'#'+(p.number||'?')+' '+p.name).join('\n');
      const input=prompt('¿De quién querés ver las pistas?\n\n'+list+'\n\nEscribí el nombre:');
      if(!input)return;
      const found=others.find(([,p])=>norm(p.name)===norm(input));
      if(!found){alert('No encontrado.');return;}
      const clues=await dg('clues/'+found[0])||[];
      const tp=PLAYERS[found[0]];
      alert(clues.length?'Pistas de '+tp.name+':\n\n'+clues.map((c,i)=>(i+1)+'. '+c.type+': '+c.value).join('\n'):tp.name+' no tiene pistas registradas.');
      const nu=uses+1;await ds('powers/'+myId,{uses:nu,used:nu>=3,maxUses:3,rol:rolName,ts:Date.now()});
    } else if(accion==='2'){
      const numStr=prompt('Ingresá el número de collar:');if(!numStr)return;
      const found2=Object.entries(PLAYERS).find(([,p])=>String(p.number)===String(numStr.trim()));
      if(!found2){alert('Número no encontrado.');return;}
      const [,fp]=found2;
      const info='El jugador #'+numStr+' pertenece a '+(fp.faccion||'facción desconocida')+'.';
      const allies=Object.entries(PLAYERS).filter(([id,p])=>id!==myId&&p.faccion===PLAYERS[myId]?.faccion);
      if(allies.length>0){const ra=allies[Math.floor(Math.random()*allies.length)];await _sys(ra[0],'📡 Tu aliado investigó: '+info,false);}
      alert('🔍 '+info+(allies.length>0?' (enviado a un aliado al azar)':''));
      const nu=uses+1;await ds('powers/'+myId,{uses:nu,used:nu>=2,maxUses:2,rol:rolName,ts:Date.now()});
    } else if(accion==='3'){
      const others=Object.entries(PLAYERS).filter(([id])=>id!==myId);
      const list=others.map(([,p])=>'#'+(p.number||'?')+' '+p.name).join('\n');
      const input=prompt('¿De quién confirmás el rol?\n(El Fantasma no puede confirmarse)\n\n'+list+'\n\nEscribí el nombre:');
      if(!input)return;
      const found3=others.find(([,p])=>norm(p.name)===norm(input));
      if(!found3){alert('No encontrado.');return;}
      const [,fp3]=found3;
      if(fp3.rol==='El Fantasma'){alert('El Fantasma no puede ser confirmado por ningún Informante.');return;}
      alert('🔍 '+fp3.name+' tiene el rol: '+(fp3.rol||'desconocido')+'.');
      await ds('powers/'+myId,{used:true,rol:rolName,ts:Date.now()});
    } else {alert('Opción no válida.');return;}
  }

  // ── ATACANTES ─────────────────────────────────────────────────
  else if(rInfo.tipo.startsWith('Atacante')){
    const others=Object.entries(PLAYERS).filter(([id])=>id!==myId);
    const list=others.map(([,p])=>'#'+(p.number||'?')+' '+p.name).join('\n');
    // El Sicario & El Agitador → bloqueo de misterios
    if(rolName==='El Sicario'||rolName==='El Agitador'){
      const input=prompt('¿A quién bloqueás de resolver misterios por 15 min?\n\n'+list+'\n\nEscribí el nombre:');
      if(!input)return;
      const found=others.find(([,p])=>norm(p.name)===norm(input));
      if(!found){alert('No encontrado.');return;}
      if(PLAYERS[found[0]]?.rol==='El Fantasma'){alert('El Fantasma es inmune. Recibió una alerta.');await _sys(found[0],'👻 Alguien intentó bloquearte. Sin efecto.',false);return;}
      await ds('blocks/'+found[0],{by:myId,until:Date.now()+900000,type:'mystery',ts:Date.now()});
      await _sys(found[0],'⛔ Fuiste bloqueado de resolver misterios por 15 minutos. El tiempo comienza ahora.',false);
      const nu=uses+1;await ds('powers/'+myId,{uses:nu,used:nu>=2,maxUses:2,rol:rolName,ts:Date.now()});
      alert('Bloqueo de 15 min aplicado a '+PLAYERS[found[0]]?.name+'.');
    }
    // El Saboteador → pista falsa en registro
    else if(rolName==='El Saboteador'){
      const input=prompt('¿En el registro de quién plantás la pista falsa?\n\n'+list+'\n\nEscribí el nombre:');
      if(!input)return;
      const found=others.find(([,p])=>norm(p.name)===norm(input));
      if(!found){alert('No encontrado.');return;}
      if(PLAYERS[found[0]]?.rol==='El Fantasma'){alert('El Fantasma es inmune.');return;}
      const cur=await dg('clues/'+found[0])||[];
      const fakeTypes=['faccion_es','faccion_no','rol_es','rol_no'];
      const ft=fakeTypes[Math.floor(Math.random()*fakeTypes.length)];
      const fakeVal=ft.includes('faccion')?FACS[Math.floor(Math.random()*FACS.length)]:Object.keys(ROLES_INFO)[Math.floor(Math.random()*Object.keys(ROLES_INFO).length)];
      cur.push({playerId:myId,type:ft,value:fakeVal,planted:true});
      await ds('clues/'+found[0],cur);
      const nu=uses+1;await ds('powers/'+myId,{uses:nu,used:nu>=2,maxUses:2,rol:rolName,ts:Date.now()});
      alert('Pista falsa plantada en el registro de '+PLAYERS[found[0]]?.name+'.');
    }
    // El Censor → pistas 50/50 a hasta 4 jugadores
    else if(rolName==='El Censor'){
      const input=prompt('¿A quién enviás la pista anónima?\n\n'+list+'\n\nEscribí el nombre:');
      if(!input)return;
      const found=others.find(([,p])=>norm(p.name)===norm(input));
      if(!found){alert('No encontrado.');return;}
      const [tid,tp]=found;const num=tp.number||'?';
      const isFalse=Math.random()<0.5;
      const kind=prompt('¿Sobre qué?\n1 - Su facción\n2 - Su rol');if(!kind)return;
      let text='';
      if(isFalse){const ff=FACS.filter(f=>f!==tp.faccion)[Math.floor(Math.random()*(FACS.length-1))];
        text=kind==='2'?'Fuente no verificada sobre el jugador #'+num+'. Tomalo con precaución.':'Rumores vinculan al jugador #'+num+' con '+ff+'.';}
      else{text=kind==='2'?'El jugador #'+num+' tiene el rol de '+(tp.rol||'desconocido')+'.':'Confirmado: el jugador #'+num+' es de '+(tp.faccion||'desconocida')+'.';}
      await _sys(tid,text,isFalse);
      const nu=uses+1;await ds('powers/'+myId,{uses:nu,used:nu>=4,maxUses:4,rol:rolName,ts:Date.now()});
      alert('Pista enviada.'+(isFalse?' (llegó falsa)':' (llegó verdadera)'));
    }
    else{alert('Este poder estará disponible durante el evento.');return;}
  }

  // ── TODOTERRENO ───────────────────────────────────────────────
  else if(rInfo.tipo==='Todoterreno'){
    const accion=prompt('¿Qué querés hacer?\n1 - Compartir un misterio resuelto con tu facción\n2 - Pedirle una pista a otro jugador');
    if(!accion)return;
    if(accion==='1'){
      const myFac=PLAYERS[myId]?.faccion;
      const myprog=await dg('mysteryProgress/'+myId)||{};
      const solved=Object.entries(GS.mysteries||{}).filter(([mid])=>myprog[mid]?.solved);
      if(!solved.length){alert('No resolviste ningún misterio todavía.');return;}
      const opts=solved.map(([,m],i)=>(i+1)+'. '+m.titulo).join('\n');
      const pick=prompt('¿Qué misterio compartís?\n\n'+opts+'\n\nEscribí el número:');if(!pick)return;
      const idx2=parseInt(pick)-1;if(idx2<0||idx2>=solved.length){alert('Opción inválida.');return;}
      const [mid,m]=solved[idx2];
      const allies=Object.entries(PLAYERS).filter(([id,p])=>id!==myId&&p.faccion===myFac);
      for(const [aid] of allies)await ds('mysteryProgress/'+aid+'/'+mid,{currentPhase:(m.phases||[]).length,solved:true});
      await ds('powers/'+myId,{used:true,rol:rolName,ts:Date.now()});
      alert('Misterio "'+m.titulo+'" compartido con toda tu facción.');
    } else if(accion==='2'){
      const others=Object.entries(PLAYERS).filter(([id])=>id!==myId);
      const list=others.map(([,p])=>'#'+(p.number||'?')+' '+p.name).join('\n');
      const input=prompt('¿A quién le pedís una pista?\n\n'+list+'\n\nEscribí el nombre:');if(!input)return;
      const found=others.find(([,p])=>norm(p.name)===norm(input));if(!found){alert('No encontrado.');return;}
      const mid2='req'+Date.now();
      await ds('clueRequests/'+found[0]+'/'+mid2,{from:myId,fromName:PLAYERS[myId]?.name||'?',ts:Date.now()});
      await _sys(found[0],'💬 '+(PLAYERS[myId]?.name||'Un jugador')+' te pide que compartas una pista. Podés aceptar o ignorar.',false);
      await ds('powers/'+myId,{used:true,rol:rolName,ts:Date.now()});
      alert('Solicitud enviada. El jugador decidirá si te da la pista.');
    } else{alert('Opción no válida.');return;}
  }

  // ── PRESTAMISTA (Comodín Mafia) ───────────────────────────────
  else if(rolName==='El Prestamista'){
    const others=Object.entries(PLAYERS).filter(([id])=>id!==myId);
    const list=others.map(([,p])=>'#'+(p.number||'?')+' '+p.name).join('\n');
    const input=prompt('¿A quién retás a un duelo?\n(Solo válido si no tenés pistas sobre ese jugador)\n\n'+list+'\n\nEscribí el nombre:');
    if(!input)return;
    const found=others.find(([,p])=>norm(p.name)===norm(input));
    if(!found){alert('No encontrado.');return;}
    const [tid,tp]=found;
    const myClues=await dg('clues/'+myId)||[];
    if(myClues.some(c=>c.playerId===tid)){alert('Tenés pistas sobre ese jugador. El duelo no es válido.');return;}
    // Show faction options
    const facOpt=prompt('¿Cuál es su facción?\n\n'+FACS.map((f,i)=>(i+1)+'. '+f).join('\n')+'\n\nEscribí el número:');
    if(!facOpt)return;
    const facIdx=parseInt(facOpt)-1;
    if(facIdx<0||facIdx>=FACS.length){alert('Opción inválida.');return;}
    const gFac=FACS[facIdx];
    // Show role options if faction guessed correctly
    const facOk=norm(gFac)===norm(tp.faccion||'');
    let rOk=false;
    if(facOk){
      const facRoles=ROLES_PRESET.filter(r=>r.fac===tp.faccion);
      const rolOpt=prompt('¡Facción correcta! Ahora elegí su rol (opcional, Enter para omitir):\n\n'+facRoles.map((r,i)=>(i+1)+'. '+r.nombre).join('\n')+'\n\nEscribí el número o dejá vacío:');
      if(rolOpt){
        const rolIdx=parseInt(rolOpt)-1;
        if(rolIdx>=0&&rolIdx<facRoles.length)rOk=norm(facRoles[rolIdx].nombre)===norm(tp.rol||'');
      }
    }
    let tPts=0;
    Object.values(SUBS).filter(s=>s.playerId===tid).forEach(sub=>Object.entries(sub.guesses||{}).forEach(([t2,g])=>{const t2p=PLAYERS[t2];if(!t2p)return;const cfg=getPTS();if(g.faccion)tPts+=norm(g.faccion)===norm(t2p.faccion)?cfg.fA:cfg.fF;if(g.rol)tPts+=norm(g.rol)===norm(t2p.rol)?cfg.rA:cfg.rF;}));
    tPts=Math.max(0,tPts);
    let stolen=0;
    if(facOk&&rOk){stolen=Math.floor(tPts*0.15);alert('🎯 Adivinaste facción Y rol. Robás el 15%: '+stolen+' pts.');}
    else if(facOk){stolen=Math.floor(tPts*0.05);alert('✓ Adivinaste la facción. Robás el 5%: '+stolen+' pts.');}
    else{alert('✗ No adivinaste. Sin efecto.');}
    if(stolen>0)await dp('submissions',{playerId:myId,phase:'duelo',guesses:{},total:stolen,ts:Date.now()});
    const nu=uses+1;await ds('powers/'+myId,{uses:nu,used:nu>=2,maxUses:2,rol:rolName,ts:Date.now()});
  }

  // ── CAMALEÓN (Comodín Agencia) ────────────────────────────────
  else if(rolName==='El Camaleón'){
    const copiedRol=pow.copiedRol;
    // If already copied a role, use it now
    if(copiedRol&&ROLES_INFO[copiedRol]){
      const confirmed=confirm('Vas a usar el poder copiado: "'+ROLES_INFO[copiedRol].poder+'" ('+copiedRol+').\n\nEste será tu único uso. ¿Confirmás?');
      if(!confirmed)return;
      // Temporarily swap role and activate
      await activatePower(myId,copiedRol);
      // Mark camaleón as used
      await ds('powers/'+myId,{used:true,rol:rolName,copiedRol,usedCopied:true,ts:Date.now()});
      return;
    }
    // Copy a new role
    const others=Object.entries(PLAYERS).filter(([id])=>id!==myId);
    const nonComodines=others.filter(([,p])=>p.rol&&ROLES_INFO[p.rol]?.tipo!=='Comodín'&&ROLES_INFO[p.rol]?.tipo!=='Reserva');
    if(!nonComodines.length){alert('No hay roles disponibles para copiar.');return;}
    const list=nonComodines.map(([,p])=>'#'+(p.number||'?')+' '+p.name).join('\n');
    const input=prompt('¿De quién copiás el poder?\n(No puede ser otro Comodín ni Reserva)\n\n'+list+'\n\nEscribí el nombre:');
    if(!input)return;
    const found=nonComodines.find(([,p])=>norm(p.name)===norm(input));
    if(!found){alert('No encontrado o no válido.');return;}
    const [,tp]=found;
    const rInf2=ROLES_INFO[tp.rol];
    await _sys(found[0],'⚠️ Alguien copió tu poder de forma anónima.',false);
    // Save copied role - next activation will use it
    await ds('powers/'+myId,{...pow,uses:uses+1,copiedRol:tp.rol,rol:rolName,ts:Date.now()});
    alert('Copiaste el poder "'+rInf2?.poder+'" de '+tp.name+'. Activá de nuevo para usarlo (se consume en ese momento).');
    rProfile();return;
  }

  // ── MINISTRO (Comodín Municipales) ───────────────────────────
  else if(rolName==='El Ministro'){
    // Don't show who are allies - player must guess
    const others=Object.entries(PLAYERS).filter(([id])=>id!==myId);
    const list=others.map(([,p])=>'#'+(p.number||'?')+' '+p.name).join('\n');
    const input=prompt('¿A quién le multiplicás los puntos de esta fase?\n(Solo funciona si elegís a un aliado de tu facción)\n\n'+list+'\n\nEscribí el nombre:');
    if(!input)return;
    const found=others.find(([,p])=>norm(p.name)===norm(input));
    if(!found){alert('No encontrado.');return;}
    const [tid,tp]=found;
    await ds('multipliers/'+tid,{by:myId,phase:GS.phase||'A',mult:2,maxBonus:8,ts:Date.now()});
    await ds('powers/'+myId,{used:true,rol:rolName,ts:Date.now()});
    alert('Multiplicador x2 activado para '+tp.name+'. Si es tu aliado, verá sus puntos duplicados al cerrar la fase.');
  }

  // ── FANTASMA ──────────────────────────────────────────────────
  else if(rolName==='El Fantasma'){
    alert('👻 Tu poder es pasivo.\n\nEl Fantasma es inmune a todos los ataques y bloqueos durante toda la noche. No se activa, ya está activo.');
    return;
  }

  // ── RESERVA ───────────────────────────────────────────────────
  else if(rInfo.tipo==='Reserva'){
    alert('Este rol no tiene habilidad asignada esta noche.');return;
  }

  else{alert('Este poder estará disponible durante el evento.');return;}

  rProfile();
};


window.markAnonRead=async(myId,mid)=>{await ds('anonMessages/'+myId+'/'+mid+'/read',true);};
window.saveCat=async()=>{
  const c=txtToC(document.getElementById('cat-ed').value);
  const cats=Object.keys(c);if(!cats.length){alert('Usá ## antes de cada categoría.');return;}
  try{await ds('gamestate/catering',c);alert('✓ Catering guardado: '+cats.join(', '));}
  catch(e){alert('Error. Verificá las reglas de Firebase.');}
};
window.saveRoles=async()=>{
  const text=document.getElementById('roles-ed').value;
  const roles=text.split('\n').map(line=>{const p=line.split('|');const n=(p[0]||'').trim();const f=(p[1]||'').trim();const num=(p[2]||'').trim();return n?{nombre:n,faccion:f,numero:num}:null;}).filter(Boolean);
  try{await ds('gamestate/roles',roles);alert('✓ '+roles.length+' roles guardados.');}
  catch(e){alert('Error al guardar.');}
};
window.savePokerRules=async()=>{
  const text=document.getElementById('poker-rules-ed')?.value||'';
  await ds('gamestate/pokerRules',text);
  alert('✓ Reglas de póker guardadas.');
};
window.saveRules2=async()=>{try{await ds('gamestate/rules',document.getElementById('rules-ed').value);alert('✓ Reglas guardadas.');}catch(e){alert('Error.');}};
window.chPin=async()=>{const pin=document.getElementById('newpin').value.trim();if(!pin)return;await ds('config/pin',pin);alert('✓ PIN actualizado.');};
window.resetSubs=async()=>{
  if(!confirm('¿Resetear el progreso del juego?\n\nEsto limpia: votos, misterios, poderes, bloqueos, mensajes anónimos, pistas, protecciones.'))return;
  await Promise.all([
    ds('submissions',null),ds('mysteryProgress',null),ds('powers',null),
    ds('blocks',null),ds('anonMessages',null),ds('clues',null),
    ds('protections',null),ds('multipliers',null),ds('duels',null),
  ]);
  alert('✓ Progreso reseteado. Perfiles y jugadores intactos.');
};
window.resetAll=async()=>{if(!confirm('⚠️ Borra TODO. ¿Seguro?'))return;await ds('/',null);await ds('config/pin','1234');};
window.addMystery=async()=>{
  const titulo=prompt('Nombre del misterio:');if(!titulo)return;
  const revelation=prompt('¿Qué revela al resolverse? (pista que verá el jugador)');
  const mys=await dg('gamestate/mysteries')||{};
  mys['m'+Date.now()]={titulo,revelation,phases:[]};
  await ds('gamestate/mysteries',mys);alert('✓ Creado. Editalo para agregar fases.');
};
window.editMystery=async mid=>{
  const mys=await dg('gamestate/mysteries')||{};const m=mys[mid];if(!m)return;
  const act=prompt(`"${m.titulo}" (${(m.phases||[]).length} fases)\n1 - Agregar fase\n2 - Borrar última`);
  if(act==='1'){
    const pista=prompt('Texto de la pista / enigma:');if(!pista)return;
    const nOpts=parseInt(prompt('¿Cuántas opciones de respuesta?')||'3');
    const opciones=[];
    for(let i=0;i<nOpts;i++){
      const texto=prompt(`Opción ${i+1}:`);
      const correcta=confirm(`"${texto}" ¿es la correcta?`);
      opciones.push({texto,correcta});
    }
    if(!m.phases)m.phases=[];m.phases.push({pista,opciones});
    mys[mid]=m;await ds('gamestate/mysteries',mys);alert('✓ Fase agregada.');
  } else if(act==='2'){
    if(!m.phases?.length){alert('No hay fases.');return;}
    m.phases.pop();mys[mid]=m;await ds('gamestate/mysteries',mys);alert('✓ Eliminada.');
  }
};
window.delMystery=async mid=>{if(!confirm('¿Eliminar misterio?'))return;const mys=await dg('gamestate/mysteries')||{};delete mys[mid];await ds('gamestate/mysteries',mys);};

function locked(msg){return`<div class="lscreen"><div class="licon">🔒</div><div class="lmsg">${msg}</div></div>`;}

// ── VER PERFIL DE OTRO JUGADOR ─────────────────────────────
window.viewPlayer=async(pid)=>{
  const _vp=PLAYERS[pid];
  if(_vp&&_vp.rol==='Famoso'&&CU&&!CU.isAdmin){
    const _fid=Object.keys(PLAYERS).find(k=>norm(PLAYERS[k].name)===norm(_vp.name));
    if(_fid){
      const mid='m'+Date.now();
      await ds('anonMessages/'+_fid+'/'+mid,{text:'\uD83D\uDC41 '+CU.name+' visit\u00f3 tu perfil.',isFalse:false,read:false,ts:Date.now()});
    }
  }
  const p=PLAYERS[pid];if(!p)return;
  const subs=SUBS;
  const mysteries=GS.mysteries||{};
  const myprog=await dg('mysteryProgress/'+pid)||{};
  const posPoints=GS.posPoints||[10,7,5,3,1];
  const pokerPhase=GS.pokerPhase||'A';
  let hits=0,errors=0,pokerPts=0;
  Object.values(subs).filter(s=>s.playerId===pid).forEach(sub=>{
    Object.entries(sub.guesses||{}).forEach(([tid,g])=>{
      const t=PLAYERS[tid];if(!t)return;
      if(g.faccion){if(norm(g.faccion)===norm(t.faccion))hits++;else errors++;}
      if(g.rol){if(norm(g.rol)===norm(t.rol))hits++;else errors++;}
    });
  });
  Object.values(TABLES).forEach(t=>{
    const pts=t.points||{};const pids=t.players||[];
    if(pokerPhase==='A'){
      const sorted=[...pids].filter(pp=>pts[pp]!==undefined).sort((a,b)=>(pts[b]||0)-(pts[a]||0));
      const idx=sorted.indexOf(pid);if(idx>=0)pokerPts+=(posPoints[idx]||0);
    } else {if(pts[pid]!==undefined)pokerPts+=pts[pid];}
  });
  const solved=Object.entries(mysteries).filter(([mid])=>myprog[mid]?.solved);

  // Navigate to p1 tab and show read-only profile
  CP='p1';
  document.querySelectorAll('.page').forEach(x=>x.classList.remove('active'));
  document.querySelectorAll('.nb').forEach(x=>x.classList.remove('active'));
  document.getElementById('p1')?.classList.add('active');
  document.querySelector('.nb[data-page="p1"]')?.classList.add('active');

  const el=document.getElementById('p1c');
  el.innerHTML=`
    <div style="display:flex;align-items:center;gap:8px;margin-bottom:14px;cursor:pointer;color:var(--muted);font-size:13px" onclick="window.rP1()">
      <svg style="width:18px;height:18px;stroke:currentColor;fill:none;stroke-width:2" viewBox="0 0 24 24"><path d="M19 12H5M12 5l-7 7 7 7" stroke-linecap="round" stroke-linejoin="round"/></svg>
      Volver
    </div>
    <div class="phead">
      <div style="font-size:28px;width:44px;height:44px;border-radius:10px;display:flex;align-items:center;justify-content:center;background:${p.faccion&&FC2[p.faccion]?FC2[p.faccion]+'18':'var(--card2)'};border:2px solid ${p.faccion&&FC2[p.faccion]?FC2[p.faccion]+'44':'var(--border)'};flex-shrink:0">${p.avatar||'🎭'}</div>
      <div style="flex:1">
        <div class="pname" style="color:${p.nameColor||'var(--gold)'}">${p.name}</div>
        ${p.apodo?`<div class="papodo">"${p.apodo}"</div>`:''}
        ${(()=>{
          const _myPid=CU&&PLAYERS?Object.keys(PLAYERS).find(k=>norm(PLAYERS[k]?.name||'')===norm(CU?.name||'')):null;
          const _gf2=CU&&CU.isAdmin?true:(_myPid&&Object.values(SUBS).some(s=>s.playerId===_myPid&&s.guesses&&s.guesses[pid]&&s.guesses[pid].faccionOk));
          return p.faccion&&_gf2?`<div style="color:${FC2[p.faccion]};font-size:12px">${FI[p.faccion]} ${p.faccion}</div>`:'<div style="font-size:11px;color:var(--muted)">Facción desconocida ❓</div>';
        })()}
      </div>
    </div>
    <div class="pstats">
      <div class="psbox"><div class="psval">${hits}</div><div class="pslbl">Aciertos</div></div>
      <div class="psbox"><div class="psval">${errors}</div><div class="pslbl">Errores</div></div>
      <div class="psbox"><div class="psval">${pokerPts}</div><div class="pslbl">Póker</div></div>
      <div class="psbox"><div class="psval">${solved.length}</div><div class="pslbl">Misterios</div></div>
    </div>
    <div class="card" style="margin-top:12px">
      <div class="cl">Perfil</div>
      ${p.nombreCompleto?`<div style="display:flex;justify-content:space-between;padding:5px 0;border-bottom:1px solid var(--border)"><span style="color:var(--muted);font-size:13px">Nombre</span><span style="font-size:14px">${p.nombreCompleto}</span></div>`:''}
      ${p.edad?`<div style="display:flex;justify-content:space-between;padding:5px 0;border-bottom:1px solid var(--border)"><span style="color:var(--muted);font-size:13px">Edad</span><span style="font-size:14px">${p.edad} años</span></div>`:''}
      ${p.civil?`<div style="display:flex;justify-content:space-between;padding:5px 0;border-bottom:1px solid var(--border)"><span style="color:var(--muted);font-size:13px">Estado civil</span><span style="font-size:14px">${p.civil}</span></div>`:''}
      ${p.bio?`<div style="padding:8px 0"><div style="color:var(--muted);font-size:12px;margin-bottom:5px">Biografía</div><div style="font-size:14px;color:var(--soft);line-height:1.6;font-style:italic">${p.bio}</div></div>`:''}
      ${!p.nombreCompleto&&!p.edad&&!p.bio?`<div style="color:var(--muted);font-size:13px;font-style:italic">Este jugador aún no completó su perfil.</div>`:''}
    </div>
    ${solved.length>0?`<div class="card">
      <div class="cl">Misterios resueltos</div>
      ${solved.map(([,m])=>`<div class="myslvrow"><span>✅ ${m.titulo||'Misterio'}</span>
        <span style="font-size:11px;color:var(--muted)">${(m.phases||[]).length} fases</span></div>`).join('')}
    </div>`:''}
    <div class="divrow"><span class="divl"></span><span class="divd">◆</span><span class="divl"></span></div>
    <button class="bgh bsm" style="width:100%;opacity:.5" onclick="showAdminModal()">🔐 Acceso organizador</button>`;
};

// Chat enabled watch
const _origRenderAll=renderAll;
window._checkChatFab=()=>{
  const fab=document.getElementById('chat-fab');
  if(fab)fab.style.display=(CU&&!CU.isAdmin&&(GS.chatEnabled||GS.testMode))?'flex':'none';
};
// Override updateNav to also check chat
const origUpdateNav=updateNav;
window.addEventListener('gamestate-updated',()=>window._checkChatFab());

window.ds=ds;
// Expose render functions to global scope for onclick handlers
window.rP1=rP1;window.rP2=rP2;window.rP3=rP3;window.rP4=rP4;window.rAdmin=rAdmin;
window.rProfile=rProfile;window.switchChatTab=switchChatTab;window.buildChatTabs=buildChatTabs;
window.sendChat=window.sendChat||sendChat;window.openChatPanel=window.openChatPanel;window.closeChatPanel=window.closeChatPanel;
</script>
</body>
</html>
