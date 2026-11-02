<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Notepad | Writing Workspace</title>
<style>
:root{--bg:#081321;--panel:#0e1e30;--panel2:#12283d;--line:#263f57;--text:#e8f0f7;--muted:#91a7ba;--accent:#6ba9df;--accent2:#367db7;--good:#78c8a5}
*{box-sizing:border-box}
body{margin:0;min-height:100vh;background:radial-gradient(ellipse at 15% 0%,#16334d 0,transparent 38%),var(--bg);color:var(--text);font-family:Inter,Segoe UI,Arial,sans-serif}
.topbar{height:72px;padding:0 5%;display:flex;align-items:center;gap:14px;border-bottom:1px solid var(--line);background:#081827e8}
.logo{width:39px;height:39px;border:1px solid #527b9e;border-radius:11px;display:grid;place-items:center;color:#b9d9f3;font-size:20px}
.brand{font-weight:750;letter-spacing:.8px}.brand small{display:block;font-size:10px;color:var(--muted);font-weight:600;letter-spacing:2px;margin-top:4px}
.top-actions{margin-left:auto;display:flex;align-items:center;gap:9px}
button{font:inherit;cursor:pointer}
.btn{border:1px solid var(--line);background:#142b40;color:#dce9f4;border-radius:8px;padding:9px 13px;font-size:12px;font-weight:650}
.btn:hover{border-color:#5b88ae;background:#1a3852}
.btn.primary{background:linear-gradient(135deg,var(--accent2),#285e8b);border-color:#4b91c8;color:white}
main{max-width:1120px;margin:32px auto;padding:0 22px 45px}
.heading{display:flex;justify-content:space-between;align-items:flex-end;gap:15px;margin-bottom:20px}
.heading h1{font-size:24px;margin:0 0 6px}.heading p{margin:0;color:var(--muted);font-size:13px}
.status{font-size:11px;color:var(--good);display:flex;align-items:center;gap:7px;white-space:nowrap}.dot{width:7px;height:7px;background:var(--good);border-radius:50%}
.workspace{background:linear-gradient(150deg,var(--panel),#0b1928);border:1px solid var(--line);border-radius:15px;overflow:hidden;box-shadow:0 20px 50px #0003}
.toolbar{display:flex;align-items:center;gap:8px;flex-wrap:wrap;padding:13px 15px;border-bottom:1px solid var(--line);background:#102238}
.mode-switch{display:flex;gap:4px;padding:4px;background:#081827;border:1px solid #29445d;border-radius:9px}
.mode{border:0;background:transparent;color:#9eb2c4;border-radius:6px;padding:8px 12px;font-size:12px;font-weight:700}
.mode.active{background:#234766;color:#f2f8fd;box-shadow:inset 0 0 0 1px #416b8d}
.separator{height:25px;width:1px;background:var(--line);margin:0 3px}
.tool{min-width:34px;height:33px;border:1px solid transparent;border-radius:6px;background:transparent;color:#d6e4ef;font-weight:700}
.tool:hover,.tool:focus{background:#1b3851;border-color:#345975}
.tool.wide{padding:0 10px;font-size:11px}
.toolbar-spacer{flex:1}
.editor-wrap{padding:22px}
.doc-title{width:100%;border:0;border-bottom:1px solid #20394f;background:transparent;color:var(--text);font-size:20px;font-weight:700;padding:4px 2px 14px;margin-bottom:15px;outline:none}
.editor{min-height:440px;max-height:65vh;overflow:auto;outline:none;color:#e2ebf3;font-size:15px;line-height:1.8;padding:4px 2px;white-space:normal;overflow-wrap:anywhere}
.editor:empty:before{content:attr(data-placeholder);color:#71899e;pointer-events:none}
.editor h1,.editor h2,.editor h3{color:#f1f6fb;line-height:1.35}
.editor blockquote{border-left:3px solid var(--accent);margin-left:0;padding-left:14px;color:#a9bfd1}
.editor code{background:#1a3045;padding:2px 5px;border-radius:4px}
.markdown{display:none;width:100%;min-height:440px;max-height:65vh;resize:vertical;border:0;outline:none;background:transparent;color:#e2ebf3;font:14px/1.8 ui-monospace,SFMono-Regular,Consolas,monospace;white-space:pre-wrap;overflow:auto}
.markdown::placeholder{color:#71899e}
.bottom{display:flex;justify-content:space-between;align-items:center;gap:12px;padding:11px 17px;border-top:1px solid var(--line);background:#0b1a29;color:#8ea5b8;font-size:11px}
.bottom strong{color:#c7d8e6;font-weight:600}
.toast{position:fixed;right:24px;bottom:24px;background:#153a32;border:1px solid #2d705d;color:#d0f3e5;padding:11px 15px;border-radius:9px;font-size:12px;opacity:0;transform:translateY(8px);transition:.2s;pointer-events:none}
.toast.show{opacity:1;transform:translateY(0)}
@media(max-width:650px){.topbar{padding:0 17px}.top-actions .btn{padding:8px}.heading{align-items:flex-start;flex-direction:column}.editor-wrap{padding:15px}.editor,.markdown{min-height:55vh}.toolbar-spacer{display:none}.bottom{align-items:flex-start;flex-direction:column}}
</style>
</head>
<body>
<header class="topbar">
  <div class="logo">✎</div>
  <div class="brand">NOTEPAD <small>WRITING WORKSPACE</small></div>
  <div class="top-actions">
    <button class="btn" id="copyBtn">Copy</button>
    <button class="btn primary" id="saveBtn">Save note</button>
  </div>
</header>
<main>
  <div class="heading">
    <div><h1>Your workspace</h1><p>A clean space to write, format and work with Markdown.</p></div>
    <div class="status"><span class="dot"></span><span id="saveStatus">Autosave enabled</span></div>
  </div>
  <section class="workspace">
    <div class="toolbar">
      <div class="mode-switch" role="tablist" aria-label="Editor mode">
        <button class="mode active" id="richMode" role="tab" aria-selected="true">Rich text</button>
        <button class="mode" id="markdownMode" role="tab" aria-selected="false">Markdown</button>
      </div>
      <span class="separator"></span>
      <div id="richTools">
        <button class="tool" data-command="bold" title="Bold (Ctrl+B)"><b>B</b></button>
        <button class="tool" data-command="italic" title="Italic (Ctrl+I)"><i>I</i></button>
        <button class="tool" data-command="underline" title="Underline (Ctrl+U)"><u>U</u></button>
        <button class="tool" data-command="insertUnorderedList" title="Bullet list">• List</button>
        <button class="tool" data-command="insertOrderedList" title="Numbered list">1. List</button>
        <button class="tool wide" data-command="formatBlock" data-value="h2" title="Heading">Heading</button>
        <button class="tool wide" data-command="formatBlock" data-value="blockquote" title="Quote">Quote</button>
        <button class="tool wide" data-command="removeFormat" title="Clear formatting">Clear format</button>
      </div>
      <div class="toolbar-spacer"></div>
      <button class="btn" id="clearBtn">Clear</button>
    </div>
    <div class="editor-wrap">
      <input class="doc-title" id="docTitle" type="text" maxlength="120" placeholder="Untitled note" aria-label="Note title">
      <div class="editor" id="richEditor" contenteditable="true" spellcheck="true" data-placeholder="Start writing here... Select text and press Ctrl+B for bold or Ctrl+I for italics."></div>
      <textarea class="markdown" id="markdownEditor" spellcheck="false" placeholder="Write Markdown here...&#10;&#10;**Bold text**&#10;*Italic text*"></textarea>
    </div>
    <div class="bottom">
      <span><strong id="modeLabel">RICH TEXT MODE</strong> · Ctrl+B bold · Ctrl+I italic</span>
      <span><span id="wordCount">0 words</span> · <span id="charCount">0 characters</span></span>
    </div>
  </section>
</main>
<div class="toast" id="toast">Copied to clipboard</div>
<script>
const richEditor = document.getElementById('richEditor');
const markdownEditor = document.getElementById('markdownEditor');
const richModeBtn = document.getElementById('richMode');
const markdownModeBtn = document.getElementById('markdownMode');
const richTools = document.getElementById('richTools');
const docTitle = document.getElementById('docTitle');
let currentMode = 'rich';
let saveTimer;

function escapeHtml(s){return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');}
function inlineHtmlToMd(node){
  if(node.nodeType===3) return node.nodeValue;
  if(node.nodeType!==1) return '';
  const tag=node.tagName.toLowerCase();
  let inner=[...node.childNodes].map(inlineHtmlToMd).join('');
  if(tag==='strong'||tag==='b') return '**'+inner+'**';
  if(tag==='em'||tag==='i') return '*'+inner+'*';
  if(tag==='u') return '<u>'+inner+'</u>';
  if(tag==='code') return '`'+inner+'`';
  if(tag==='br') return '\n';
  if(tag==='a') return inner;
  return inner;
}
function htmlToMarkdown(root){
  function block(node){
    if(node.nodeType===3) return node.nodeValue;
    if(node.nodeType!==1) return '';
    const tag=node.tagName.toLowerCase();
    if(tag==='ul'||tag==='ol'){
      const items=[...node.children].filter(x=>x.tagName.toLowerCase()==='li').map((li,i)=>(tag==='ul'?'- ':`${i+1}. `)+[...li.childNodes].map(inlineHtmlToMd).join('').trim());
      return items.join('\n')+'\n\n';
    }
    let content=[...node.childNodes].map(inlineHtmlToMd).join('').trim();
    if(tag==='h1') return '# '+content+'\n\n';
    if(tag==='h2') return '## '+content+'\n\n';
    if(tag==='h3') return '### '+content+'\n\n';
    if(tag==='blockquote') return content.split('\n').map(x=>'> '+x).join('\n')+'\n\n';
    if(tag==='div'||tag==='p') return content+'\n\n';
    if(tag==='br') return '\n';
    return content;
  }
  return [...root.childNodes].map(block).join('').replace(/\n{3,}/g,'\n\n').trim();
}
function markdownInlineToHtml(text){
  let s=escapeHtml(text);
  s=s.replace(/`([^`]+)`/g,'<code>$1</code>');
  s=s.replace(/\*\*([^*]+)\*\*/g,'<strong>$1</strong>');
  s=s.replace(/(^|[^*])\*([^*\n]+)\*(?!\*)/g,'$1<em>$2</em>');
  return s;
}
function markdownToHtml(md){
  const lines=md.split(/\r?\n/);let out=[];let listType=null;let listItems=[];
  function closeList(){if(listType){out.push('<'+listType+'>'+listItems.join('')+'</'+listType+'>');listType=null;listItems=[];}}
  for(const line of lines){
    const ul=line.match(/^\s*[-*+]\s+(.+)$/);const ol=line.match(/^\s*\d+\.\s+(.+)$/);
    if(ul||ol){const next=ul?'ul':'ol';if(listType!==next){closeList();listType=next;}listItems.push('<li>'+markdownInlineToHtml((ul||ol)[1])+'</li>');continue;}
    closeList();
    if(!line.trim()){continue;}
    const heading=line.match(/^(#{1,3})\s+(.+)$/);
    const quote=line.match(/^>\s?(.*)$/);
    if(heading){const level=heading[1].length;out.push(`<h${level}>${markdownInlineToHtml(heading[2])}</h${level}>`);}
    else if(quote){out.push('<blockquote>'+markdownInlineToHtml(quote[1])+'</blockquote>');}
    else out.push('<p>'+markdownInlineToHtml(line)+'</p>');
  }
  closeList();return out.join('');
}
function setMode(mode){
  if(mode===currentMode)return;
  if(mode==='markdown'){
    markdownEditor.value=htmlToMarkdown(richEditor);
    richEditor.style.display='none';richTools.style.display='none';markdownEditor.style.display='block';
    richModeBtn.classList.remove('active');markdownModeBtn.classList.add('active');
    richModeBtn.setAttribute('aria-selected','false');markdownModeBtn.setAttribute('aria-selected','true');
    document.getElementById('modeLabel').textContent='MARKDOWN MODE';
  }else{
    richEditor.innerHTML=markdownToHtml(markdownEditor.value);
    markdownEditor.style.display='none';richEditor.style.display='block';richTools.style.display='block';
    markdownModeBtn.classList.remove('active');richModeBtn.classList.add('active');
    markdownModeBtn.setAttribute('aria-selected','false');richModeBtn.setAttribute('aria-selected','true');
    document.getElementById('modeLabel').textContent='RICH TEXT MODE';
  }
  currentMode=mode;updateCounts();scheduleSave();
}
richModeBtn.addEventListener('click',()=>setMode('rich'));
markdownModeBtn.addEventListener('click',()=>setMode('markdown'));
document.querySelectorAll('[data-command]').forEach(btn=>btn.addEventListener('mousedown',e=>e.preventDefault()));
document.querySelectorAll('[data-command]').forEach(btn=>btn.addEventListener('click',()=>{
  richEditor.focus();const cmd=btn.dataset.command;document.execCommand(cmd,false,btn.dataset.value||null);updateCounts();scheduleSave();
}));
richEditor.addEventListener('keydown',e=>{
  if((e.ctrlKey||e.metaKey)&&['b','i','u'].includes(e.key.toLowerCase())){
    e.preventDefault();document.execCommand(({b:'bold',i:'italic',u:'underline'})[e.key.toLowerCase()],false,null);scheduleSave();
  }
});
function activeText(){return currentMode==='rich'?richEditor.innerText:markdownEditor.value;}
function updateCounts(){
  const t=activeText().trim();const words=t?t.split(/\s+/).length:0;
  document.getElementById('wordCount').textContent=words+' words';
  document.getElementById('charCount').textContent=activeText().length+' characters';
}
function scheduleSave(){clearTimeout(saveTimer);document.getElementById('saveStatus').textContent='Unsaved changes';saveTimer=setTimeout(saveNote,500);}
function saveNote(){
  const data={title:docTitle.value,mode:currentMode,rich:richEditor.innerHTML,markdown:markdownEditor.value};
  try{localStorage.setItem('cleanNotepadWorkspace',JSON.stringify(data));document.getElementById('saveStatus').textContent='Saved on this device';}
  catch(e){document.getElementById('saveStatus').textContent='Unable to save';}
}
function loadNote(){
  try{const data=JSON.parse(localStorage.getItem('cleanNotepadWorkspace')||'null');if(!data)return;
    docTitle.value=data.title||'';richEditor.innerHTML=data.rich||'';markdownEditor.value=data.markdown||'';
    if(data.mode==='markdown'){currentMode='rich';setMode('markdown');}
  }catch(e){}
}
document.getElementById('saveBtn').addEventListener('click',saveNote);
docTitle.addEventListener('input',scheduleSave);
richEditor.addEventListener('input',()=>{updateCounts();scheduleSave();});
markdownEditor.addEventListener('input',()=>{updateCounts();scheduleSave();});
document.getElementById('clearBtn').addEventListener('click',()=>{
  if(!confirm('Clear the current note content?'))return;
  richEditor.innerHTML='';markdownEditor.value='';updateCounts();scheduleSave();
});
document.getElementById('copyBtn').addEventListener('click',async()=>{
  const text=currentMode==='rich'?htmlToMarkdown(richEditor):markdownEditor.value;
  try{await navigator.clipboard.writeText(text);showToast('Copied note as Markdown');}
  catch(e){showToast('Clipboard access unavailable — select and copy the text');}
});
function showToast(message){const t=document.getElementById('toast');t.textContent=message;t.classList.add('show');setTimeout(()=>t.classList.remove('show'),1900);}
loadNote();updateCounts();
</script>
</body>
</html>
