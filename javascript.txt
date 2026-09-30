// INSTITUTO CORES DO BRASIL - JS corrigido
window.fecharCaixas = function(){ 
  document.querySelectorAll('.caixa-conteudo').forEach(c => c.style.display = 'none'); 
};

function mostrarTrofeu(){
  criarModalTrofeu();
  document.getElementById('modal-trofeu').style.display = 'block';
}

function criarModalTrofeu(){
  if(document.getElementById('modal-trofeu')) return;
  const modal = document.createElement('div');
  modal.id = 'modal-trofeu';
  modal.style.display = 'none';
  modal.innerHTML = `
    <div style="position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.6); display:flex; align-items:center; justify-content:center; z-index:9999;">
      <div style="background:white; padding:2.5rem; border-radius:20px; text-align:center; max-width:350px; width:90%; border-top:8px solid #FEDF00; border-bottom:8px solid #009739;">
        <div style="font-size:80px;">🏆</div>
        <h2 style="color:#002776; margin:1rem 0;">Cadastro realizado com sucesso!</h2>
        <p>Obrigado por fazer parte do<br><strong>Instituto Cores do Brasil</strong> 💚💛💙</p>
        <button id="btn-fecha-trofeu" style="margin-top:1.5rem; background:#009739; color:white; border:none; padding:.8rem 2rem; border-radius:30px; font-weight:800; cursor:pointer;">Fechar</button>
      </div>
    </div>`;
  document.body.appendChild(modal);
  document.getElementById('btn-fecha-trofeu').addEventListener('click', ()=>{
    modal.style.display = 'none';
  });
}

// Tudo que mexe no DOM espera carregar
document.addEventListener('DOMContentLoaded', () => {
  // 1. Fix logo
  const style = document.createElement('style');
  style.innerHTML = `
    .logo-container{display:flex !important; align-items:center !important; justify-content:center !important; overflow:visible !important;}
    .heart{-webkit-transform:rotate(-45deg) !important; transform:rotate(-45deg) !important; flex-shrink:0 !important; display:block !important;}
    .heart::before,.heart::after{display:block !important; content:"" !important;}
    .menu-btn, .btn-enviar, .btn-fechar, .trabalhe-btn-footer{cursor:pointer !important;}
  `;
  document.head.appendChild(style);

  // 2. Menu
  document.querySelectorAll('.menu-btn').forEach(btn => {
    btn.addEventListener('click', () => {
      window.fecharCaixas();
      const box = document.getElementById('box-' + btn.dataset.target);
      if(box){
        box.style.display = 'block';
        box.scrollIntoView({behavior:'smooth', block:'start'});
      }
    });
  });

  // 3. Forms
  const boxProjetos = document.getElementById('box-projetos');
  if(boxProjetos) boxProjetos.style.display = 'block';

  document.getElementById('form-voluntario')?.addEventListener('submit', e => {
    e.preventDefault(); window.fecharCaixas(); e.target.reset(); mostrarTrofeu();
  });
  document.getElementById('form-pcd')?.addEventListener('submit', e => {
    e.preventDefault(); e.target.reset();
    document.getElementById('form-pcd-box').style.display = 'none';
    mostrarTrofeu();
  });
  document.getElementById('form-trabalhe')?.addEventListener('submit', e => {
    e.preventDefault(); e.target.reset();
    document.getElementById('box-trabalhe').style.display = 'none';
    mostrarTrofeu();
  });
  document.getElementById('btn-inscrever-pcd')?.addEventListener('click', () => {
    const f = document.getElementById('form-pcd-box');
    f.style.display = 'block'; f.scrollIntoView({behavior:'smooth'});
  });
  document.getElementById('btn-trabalhe-footer')?.addEventListener('click', () => {
    const box = document.getElementById('box-trabalhe');
    box.style.display = box.style.display === 'block' ? 'none' : 'block';
  });
});