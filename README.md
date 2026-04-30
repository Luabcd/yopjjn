<!DOCTYPE html>
<html>
<body>

<h3>注册</h3>
<input id="u"><input id="p">
<button onclick="reg()">注册</button>

<h3>登录</h3>
<button onclick="login()">登录</button>

<h3>卡密</h3>
<input id="key">
<button onclick="use()">使用</button>

<h3>聊天</h3>
<input id="msg">
<button onclick="send()">发送</button>

<pre id="out"></pre>

<script>
let token = "";
let ws;

function dev(){
  let d = localStorage.getItem("d");
  if(!d){ d="dev_"+Math.random(); localStorage.setItem("d",d); }
  return d;
}

async function reg(){
  await fetch("/register",{method:"POST",
    headers:{"Content-Type":"application/json"},
    body:JSON.stringify({username:u.value,password:p.value})});
}

async function login(){
  let r = await fetch("/login",{method:"POST",
    headers:{"Content-Type":"application/json"},
    body:JSON.stringify({username:u.value,password:p.value})});
  let j = await r.json();
  token = j.token;

  ws = new WebSocket("ws://localhost:3000?id=1");
  ws.onmessage = e=>{
    let d = JSON.parse(e.data);
    out.textContent += "\nAI:"+d.message;
  };
}

async function use(){
  let r = await fetch("/use",{method:"POST",
    headers:{"Content-Type":"application/json","Authorization":token},
    body:JSON.stringify({key:key.value,device:dev()})});
  out.textContent += "\n"+JSON.stringify(await r.json());
}

function send(){
  ws.send(JSON.stringify({message:msg.value}));
  out.textContent += "\n我:"+msg.value;
}
</script>

</body>
</html>