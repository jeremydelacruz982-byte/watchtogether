<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Watch Together</title>
<style>
:root{--bg:#faf7f5;--card:#fff;--ink:#241f1f;--mut:#7a6f6f;--line:#e8dfdb;--acc:#d6456b;--acc2:#fff;--warn:#b45309;--ok:#15803d;color-scheme:light;
box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#161214;--card:#211b1e;--ink:#f3ecee;--mut:#a39499;--line:#352c30;--acc:#ec6a8e;--acc2:#1a1114;--warn:#f5a524;--ok:#4ade80;color-scheme:dark}}
:root[data-theme="dark"]{--bg:#161214;--card:#211b1e;--ink:#f3ecee;--mut:#a39499;--line:#352c30;--acc:#ec6a8e;--acc2:#1a1114;--warn:#f5a524;--ok:#4ade80;color-scheme:dark}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--ink);font:15px/1.5 system-ui,-apple-system,"Segoe UI",Roboto,sans-serif}
.wrap{max-width:1100px;margin:0 auto;padding:16px}
h1{font-size:22px;margin:0}
.mut{color:var(--mut)}
.card{background:var(--card);border:1px solid var(--line);border-radius:14px;padding:16px}
button,input{font:inherit;color:inherit}
button{cursor:pointer;border:1px solid var(--line);background:var(--card);border-radius:10px;padding:8px 14px}
button.pri{background:var(--acc);color:var(--acc2);border-color:var(--acc);font-weight:600}
button:disabled{opacity:.5;cursor:not-allowed}
input[type=text]{border:1px solid var(--line);background:var(--bg);border-radius:10px;padding:9px 12px;width:100%}
#lobby{max-width:460px;margin:8vh auto 0;text-align:center}
#lobby .row{display:flex;gap:8px;margin-top:10px}
.stack{display:grid;gap:12px;margin-top:18px;text-align:left}
#room{display:none}
.top{display:flex;gap:10px;align-items:center;justify-content:space-between;flex-wrap:wrap;margin-bottom:12px}
.code{font:600 18px ui-monospace,Menlo,Consolas,monospace;letter-spacing:.12em;background:var(--card);border:1px solid var(--line);border-radius:10px;padding:5px 12px;user-select:all}
.grid{display:grid;grid-template-columns:minmax(0,1fr) 320px;gap:14px}
@media (max-width:820px){.grid{grid-template-columns:1fr}}
.stage{background:#000;border-radius:14px;overflow:hidden;position:relative;aspect-ratio:16/9;display:flex;align-items:center;justify-content:center}
video{width:100%;height:100%;background:#000;display:none}
#drop{color:#ddd;text-align:center;padding:20px}
#drop button{margin-top:10px}
.stage.over{outline:3px dashed var(--acc)}
.bar{display:flex;gap:8px;align-items:center;flex-wrap:wrap;margin-top:10px}
.pill{font-size:13px;padding:3px 10px;border-radius:99px;border:1px solid var(--line);background:var(--card)}
.warn{color:var(--warn)} .ok{color:var(--ok)}
#alert{display:none;margin-top:10px;padding:10px 12px;border-radius:10px;border:1px solid var(--warn);color:var(--warn)}
.side{display:flex;flex-direction:column;gap:12px;min-width:0}
#people div{display:flex;justify-content:space-between;gap:8px;padding:3px 0}
#chat{height:260px;overflow-y:auto;display:flex;flex-direction:column;gap:6px;padding:2px}
.msg{max-width:88%;padding:6px 10px;border-radius:12px;background:var(--bg);border:1px solid var(--line);overflow-wrap:anywhere}
.msg.me{align-self:flex-end;background:var(--acc);color:var(--acc2);border-color:var(--acc)}
.msg small{display:block;opacity:.75;font-size:11px}
.react{display:flex;gap:6px;flex-wrap:wrap;margin-top:8px}
.react button{padding:4px 10px;font-size:18px}
.fly{position:absolute;bottom:14%;font-size:34px;animation:up 2.2s ease-out forwards;pointer-events:none}
@keyframes up{to{transform:translateY(-180px);opacity:0}}
#toast{position:fixed;left:50%;bottom:calc(20px + env(safe-area-inset-bottom,0px));transform:translateX(-50%);background:var(--ink);color:var(--bg);padding:8px 14px;border-radius:10px;display:none;z-index:5}
</style>
</head>
<body>
<div class="wrap">

<section id="lobby" class="card"><h1>🍿 Watch Together</h1><p class="mut" id="lobbyMsg">Connecting to the room…</p><p id="lobbyErr" class="warn" style="display:none;margin:0"></p></section>

<section id="room">
  <div class="top">
    <div style="display:flex;gap:10px;align-items:center;flex-wrap:wrap">
      <strong>🍿 Watch Together</strong><span class="pill" id="role"></span><input type="text" id="nick" maxlength="20" style="width:140px" aria-label="Your name"><button id="copy">Copy invite link</button>
    </div>
    <div style="display:flex;gap:10px;align-items:center">
      <span class="pill" id="conn">connecting…</span>
    </div>
  </div>

  <div class="grid">
    <div>
      <div class="stage" id="stage">
        <video id="v" controls playsinline></video>
        <div id="drop">
          <div style="font-size:40px">🎬</div>
          <div id="dropTxt">Choose the video file</div>
          <div class="mut" style="font-size:13px">MP4 or WebM plays most reliably. Drag a file here, too.</div>
          <button class="pri" id="watch" style="display:none;margin-right:8px">▶ Watch host’s live stream</button><button class="pri" id="pick">Choose video file</button>
          <div id="liveInfo" class="mut" style="font-size:13px;margin-top:8px"></div>
          <input type="file" id="file" accept="video/*,audio/*" hidden>
        </div>
      </div>
      <div class="bar">
        <span class="pill" id="sync">no partner yet</span>
        <button id="resync" style="display:none">Resync to partner</button>
        <button id="swap" style="display:none">Change file</button>
      </div>
      <div id="alert"></div>
    </div>

    <div class="side">
      <div class="card"><strong>In this room</strong><div id="people" style="margin-top:6px"></div></div>
      <div class="card">
        <strong>Chat</strong>
        <div id="chat" style="margin:8px 0"></div>
        <div style="display:flex;gap:8px"><input type="text" id="say" maxlength="500" placeholder="Say something…"><button class="pri" id="send">Send</button></div>
        <div class="react" id="react"></div>
      </div>
    </div>
  </div>
</section>

</div>
<div id="toast"></div>

<script>
(function(){
  var $=function(id){return document.getElementById(id)};
  var v=$('v'), R=null, rn=null, code=null, file=null, quietUntil=0, lastPres=0;
  var myName='',host=false,pcs={},stream=null,lv='idle',rpc=null,hostLabel=null,bufs={},joinedEpoch=0,epoch=0,ctimer=0;
  var ICE=[{urls:'stun:stun.l.google.com:19302'},{urls:'stun:stun1.l.google.com:19302'}];
  try{myName=localStorage.getItem('wt_name')||''}catch(e){}
  $('nick').value=myName;

  function toast(t){var el=$('toast');el.textContent=t;el.style.display='block';clearTimeout(toast.h);toast.h=setTimeout(function(){el.style.display='none'},3200)}
  function nm(){var n=$('nick').value.trim().slice(0,20)||'Guest';myName=n;try{localStorage.setItem('wt_name',n)}catch(e){}return n}
  function mkCode(){var a='abcdefghjkmnpqrstuvwxyz23456789',s='';var b=new Uint8Array(6);crypto.getRandomValues(b);for(var i=0;i<6;i++)s+=a[b[i]%a.length];return s}
  function lobbyErr(t){var e=$('lobbyErr');e.textContent=t;e.style.display=t?'block':'none'}
  function now(){return Date.now()}
  function fmt(s){s=Math.max(0,Math.floor(s));var h=Math.floor(s/3600),m=Math.floor(s%3600/60),x=s%60;return (h?h+':'+String(m).padStart(2,'0'):m)+':'+String(x).padStart(2,'0')}

  // Capability is resolved asynchronously; the page renders fully without it.
  var roomReady=(window.claude&&window.claude.use)?window.claude.use('room').then(function(r){R=r;return r}).catch(function(){return null}):Promise.resolve(null);

  async function enter(){
    var r=await roomReady;
    if(!r){$('lobbyMsg').style.display='none';lobbyErr('Live rooms aren’t available in this view. Open this page through the link the host shared, while signed in.');return}
    try{rn=await r.join('wt-main')}catch(e){$('lobbyMsg').style.display='none';lobbyErr('Couldn’t open the room ('+(e&&e.code||'error')+'). Reload to retry.');return}
    try{var u=await window.claude.use('user');host=u?!!(await u.canEdit()):false}catch(e){host=false}
    if(!myName)myName=host?'Host':'Partner';
    $('nick').value=myName;
    $('dropTxt').textContent=host?'Choose the video to stream to your partner':'Wait for the host’s stream, or choose your own copy of the file';
    $('role').textContent=host?'You’re the host':'Host controls playback';
    $('lobby').style.display='none';$('room').style.display='block';
    wire();pres();
  }

  function pres(){
    if(!rn)return;
    lastPres=now();
    var p={n:myName,t:+(v.currentTime||0).toFixed(2),p:!v.paused&&!v.ended,h:host,live:host&&!!stream,e:epoch,w:lv==='live'};
    p.f=file?{n:file.name,s:file.size,d:Math.round(v.duration||0)}:null;
    rn.presence(p).catch(function(){});
  }
  function send(a){
    if(!rn||!host||now()<quietUntil)return;
    rn.emit('sync',{a:a,t:+v.currentTime.toFixed(2),p:!v.paused}).catch(function(){});
    pres();
  }

  function apply(d){
    if(lv==='live')return;
    if(!file){toast('Your partner pressed '+(d.a||'play')+' — choose the video file to follow along');return}
    quietUntil=now()+900;
    try{
      if(Math.abs(v.currentTime-d.t)>0.4)v.currentTime=d.t;
      if(d.a==='pause'||d.p===false){if(!v.paused)v.pause()}
      else if(v.paused){var pr=v.play();if(pr&&pr.catch)pr.catch(function(){toast('Tap play to join — your browser blocked autoplay')})}
    }catch(e){}
    setTimeout(pres,300);
  }

  function partner(){
    if(!rn)return null;
    var ps=rn.peers().filter(function(p){return !p.isMe});
    return ps.length?ps:null;
  }
  function est(p){var t=+p.presence.t||0;return t+(p.presence.p?(now()-p.updatedAt)/1000:0)}

  function render(){
    if(!rn)return;
    var wb=$('watch'),hp=!host&&rn.peers().filter(function(p){return !p.isMe&&p.presence.h&&p.presence.live})[0];
    wb.style.display=(hp&&!file&&lv!=='live'&&lv!=='connecting')?'inline-block':'none';
    if(hp&&(lv==='live'||lv==='connecting')&&(hp.peer!==hostLabel||(hp.presence.e||0)!==joinedEpoch))startWatch();
    var all=rn.peers(),box=$('people');box.textContent='';
    all.forEach(function(p){
      var d=document.createElement('div'),a=document.createElement('span'),b=document.createElement('span');
      var nme=String(p.presence.n||'Guest').slice(0,20);
      a.textContent=nme+(p.isMe&&p.sameTab?' (you)':p.isMe?' (you, other tab)':'');
      b.className='mut';
      b.textContent=p.presence.f?(p.presence.p?'▶ '+fmt(est(p)):'⏸ '+fmt(+p.presence.t||0)):'no file yet';
      d.appendChild(a);d.appendChild(b);box.appendChild(d);
    });
    var others=all.filter(function(p){return !p.isMe}),s=$('sync'),al=$('alert'),rs=$('resync');
    rs.style.display='none';al.style.display='none';
    if(!others.length){s.textContent=host?'waiting for your partner to open the link…':'waiting for the host…';s.className='pill';return}
    var o=others.filter(function(p){return host?!p.presence.h:p.presence.h})[0]||others[0];
    if(host&&o.presence.w){s.textContent='streaming to '+String(o.presence.n||'partner').slice(0,20);s.className='pill ok';return}
    if(!host&&lv==='live'){s.textContent='watching live';s.className='pill ok';return}
    if(file&&o.presence.f&&(o.presence.f.n!==file.name||o.presence.f.s!==file.size)){
      s.textContent='different files';s.className='pill warn';
      al.style.display='block';al.textContent='File mismatch: you have “'+file.name+'”, '+String(o.presence.n||'your partner')+' has “'+String(o.presence.f.n).slice(0,80)+'”. Syncing only works well when both of you use the identical file.';
      return;
    }
    if(!file||!o.presence.f){s.textContent=!file?'choose your file':(host?'waiting for partner to press Watch':'host hasn’t picked a file');s.className='pill';return}
    var drift=Math.abs(v.currentTime-est(o));
    if((o.presence.p||!v.paused)&&drift>2.5||(!o.presence.p&&v.paused&&drift>1.5)){
      s.textContent='out of sync by '+drift.toFixed(1)+'s';s.className='pill warn';rs.style.display=host?'none':'inline-block';
    }else{s.textContent='in sync';s.className='pill ok'}
  }

  function addMsg(who,text,me){
    var c=$('chat'),m=document.createElement('div'),s=document.createElement('small');
    m.className='msg'+(me?' me':'');s.textContent=me?'You':who;m.appendChild(s);m.appendChild(document.createTextNode(text));
    c.appendChild(m);c.scrollTop=c.scrollHeight;
    while(c.children.length>200)c.removeChild(c.firstChild);
  }
  function fly(e){
    var el=document.createElement('div');el.className='fly';el.textContent=e;el.style.left=(10+Math.random()*80)+'%';
    $('stage').appendChild(el);setTimeout(function(){el.remove()},2300);
  }


  // ---- live streaming (WebRTC), signaling over the room ----
  function myPeer(){var m=rn&&rn.peers().filter(function(p){return p.isMe&&p.sameTab})[0];return m&&m.peer}
  async function rsend(to,k,obj){
    var str=JSON.stringify(obj||{}),id=Math.random().toString(36).slice(2,8),n=Math.max(1,Math.ceil(str.length/2800));
    for(var i=0;i<n;i++){
      try{await rn.emit('rtc',{to:to,k:k,id:id,i:i,n:n,d:str.slice(i*2800,(i+1)*2800)})}catch(e){}
      if(n>1)await new Promise(function(r){setTimeout(r,70)});
    }
  }
  function onRtc(m){
    var d=m.data;if(m.isMe||!d||d.to!==myPeer())return;
    if(typeof d.d!=='string'||typeof d.id!=='string'||!(d.n>=1&&d.n<=8)||!(d.i>=0&&d.i<d.n))return;
    var key=m.peer+d.id,b=bufs[key]||(bufs[key]={n:d.n,p:[],c:0});
    if(b.p[d.i]===undefined){b.p[d.i]=d.d;b.c++}
    if(b.c<b.n)return;
    delete bufs[key];
    var o;try{o=JSON.parse(b.p.join(''))}catch(e){return}
    handleRtc(m.peer,String(d.k),o).catch(function(){});
  }
  async function addIce(pc,c){
    if(!pc)return;
    if(pc.remoteDescription){try{await pc.addIceCandidate(c)}catch(e){}}else{(pc._q=pc._q||[]).push(c)}
  }
  async function flushIce(pc){var q=pc._q||[];pc._q=[];for(var i=0;i<q.length;i++){try{await pc.addIceCandidate(q[i])}catch(e){}}}
  async function handleRtc(peer,k,o){
    if(host){
      if(k==='hello')hostOpen(peer);
      else if(k==='answer'&&pcs[peer]){await pcs[peer].setRemoteDescription(o);flushIce(pcs[peer])}
      else if(k==='ice')addIce(pcs[peer],o);
    }else{
      if(k==='offer')await partnerAnswer(peer,o);
      else if(k==='ice')addIce(rpc,o);
    }
  }
  function closePc(peer){var pc=pcs[peer];if(pc){try{pc.close()}catch(e){}delete pcs[peer]}}
  function hostOpen(peer){
    if(!host||!stream)return;
    closePc(peer);
    var pc=new RTCPeerConnection({iceServers:ICE});pcs[peer]=pc;
    pc.onicecandidate=function(e){if(e.candidate)rsend(peer,'ice',e.candidate.toJSON())};
    pc.onconnectionstatechange=function(){if(pc.connectionState==='failed'||pc.connectionState==='closed'){if(pcs[peer]===pc)delete pcs[peer];if(pc.connectionState==='failed')toast('Live stream to your partner failed')}};
    pc.onnegotiationneeded=async function(){try{var of=await pc.createOffer();await pc.setLocalDescription(of);rsend(peer,'offer',{type:of.type,sdp:of.sdp})}catch(e){}};
    stream.getTracks().forEach(function(t){pc.addTrack(t,stream)});
  }
  async function partnerAnswer(peer,offer){
    if(rpc)try{rpc.close()}catch(e){}
    var pc=rpc=new RTCPeerConnection({iceServers:ICE});
    pc.onicecandidate=function(e){if(e.candidate)rsend(peer,'ice',e.candidate.toJSON())};
    pc.ontrack=function(e){
      if(v.srcObject!==e.streams[0])v.srcObject=e.streams[0];
      v.style.display='block';$('drop').style.display='none';setLive('live');
      var pr=v.play();if(pr&&pr.catch)pr.catch(function(){toast('Tap play to start the stream')});
    };
    pc.onconnectionstatechange=function(){if(pc===rpc){if(pc.connectionState==='failed')setLive('failed');else if(pc.connectionState==='connected')setLive('live')}};
    await pc.setRemoteDescription(offer);flushIce(pc);
    var a=await pc.createAnswer();await pc.setLocalDescription(a);
    rsend(peer,'answer',{type:a.type,sdp:a.sdp});
  }
  function setLive(x){
    lv=x;var i=$('liveInfo');
    i.textContent=x==='connecting'?'Connecting to the host’s stream…':x==='failed'?'Couldn’t connect the live stream (your network may block it). You can choose your own copy of the file instead; playback will sync from the host.':'';
    if(x==='failed')$('watch').textContent='Try live stream again';
    pres();render();
  }
  function startWatch(){
    var hp=rn.peers().filter(function(p){return !p.isMe&&p.presence.h&&p.presence.live})[0];
    if(!hp){toast('The host isn’t streaming yet');return}
    hostLabel=hp.peer;joinedEpoch=hp.presence.e||0;
    setLive('connecting');rsend(hp.peer,'hello',{});
    clearTimeout(ctimer);ctimer=setTimeout(function(){if(lv==='connecting')setLive('failed')},20000);
  }

  var wired=false;
  function wire(){
    if(wired)return;wired=true;
    rn.on('sync',function(m){if(m.isMe||!m.data)return;var d=m.data;if(typeof d.t!=='number')return;apply({a:String(d.a),t:d.t,p:d.p})});
    rn.on('chat',function(m){var d=m.data||{};if(typeof d.x!=='string')return;addMsg(String(d.n||'Guest').slice(0,20),d.x.slice(0,500),m.isMe)});
    rn.on('react',function(m){var d=m.data||{};if(['❤️','😂','😮','👏','😭','🔥'].indexOf(d.e)>-1)fly(d.e)});
    rn.on('rtc',onRtc);
    rn.onPeers(function(ch){if(host)ch.left.forEach(function(p){closePc(p.peer)});render()});
    rn.onConnection(function(c){var e=$('conn');e.textContent=c?'connected':'reconnecting…';e.className='pill '+(c?'ok':'warn');$('send').disabled=!c});
    clearInterval(wire.h);wire.h=setInterval(function(){if(!v.paused&&now()-lastPres>2000)pres();render()},1000);
  }

  function load(f){
    if(!f)return;
    if(file)try{URL.revokeObjectURL(v.src)}catch(e){}
    if(rpc){try{rpc.close()}catch(e){}rpc=null}
    if(lv!=='idle'){lv='idle';$('liveInfo').textContent=''}
    v.srcObject=null;
    file=f;v.src=URL.createObjectURL(f);v.style.display='block';$('drop').style.display='none';$('swap').style.display='inline-block';
    v.onloadedmetadata=function(){
      if(host){
        Object.keys(pcs).forEach(closePc);stream=null;
        try{stream=(v.captureStream||v.mozCaptureStream).call(v);stream.onaddtrack=function(e){Object.keys(pcs).forEach(function(k){try{pcs[k].addTrack(e.track,stream)}catch(x){}})};epoch=now()}
        catch(e){toast('This browser can’t stream a local file. Use Chrome, Edge or Firefox on desktop to host.')}
      }
      pres();render()};
    v.onerror=function(){toast('This browser can’t play that file. Try MP4 (H.264) or WebM.')};
  }
  $('pick').onclick=function(){$('file').click()};
  $('swap').onclick=function(){$('file').click()};
  $('file').onchange=function(){load(this.files[0]);this.value=''};
  var st=$('stage');
  st.ondragover=function(e){e.preventDefault();st.classList.add('over')};
  st.ondragleave=function(){st.classList.remove('over')};
  st.ondrop=function(e){e.preventDefault();st.classList.remove('over');load(e.dataTransfer.files[0])};

  v.addEventListener('play',function(){send('play')});
  v.addEventListener('pause',function(){if(!v.ended)send('pause')});
  v.addEventListener('seeked',function(){send('seek')});

  $('resync').onclick=function(){
    var o=partner();if(!o)return;var p=o.filter(function(x){return x.presence.h})[0]||o[0];
    apply({a:p.presence.p?'play':'pause',t:est(p),p:!!p.presence.p});
  };

  function say(){
    var i=$('say'),t=i.value.trim();if(!t||!rn)return;
    rn.emit('chat',{n:myName,x:t.slice(0,500)}).catch(function(){toast('Message not sent')});i.value='';
  }
  $('send').onclick=say;
  $('say').onkeydown=function(e){if(e.key==='Enter')say()};
  ['❤️','😂','😮','👏','😭','🔥'].forEach(function(e){
    var b=document.createElement('button');b.textContent=e;b.onclick=function(){if(rn)rn.emit('react',{e:e}).catch(function(){})};$('react').appendChild(b);
  });

  $('watch').onclick=startWatch;
  $('nick').onchange=function(){nm();pres()};
  $('copy').onclick=function(){
    var txt='Join me on Watch Together: '+location.href.split('#')[0];
    (navigator.clipboard?navigator.clipboard.writeText(txt):Promise.reject()).then(function(){toast('Invite copied')},function(){toast('Copy blocked — share the page link directly')});
  };
  enter();
})();
</script>
</body>
</html>
