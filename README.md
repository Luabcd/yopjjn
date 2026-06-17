<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>常用链接汇总</title>
    <style>
        *{margin:0;padding:0;box-sizing:border-box;font-family:system-ui, sans-serif;transition: background 0.3s, color 0.3s;}
        :root{
            --bg-color: #f5f7fa;
            --card-bg: #ffffff;
            --text-color: #222222;
            --border-color: #eeeeee;
            --primary: #409eff;
            --danger: #f56c6c;
        }
        [data-theme="dark"]{
            --bg-color: #1a1a2e;
            --card-bg: #252542;
            --text-color: #eeeeee;
            --border-color: #3a3a5c;
        }
        body{background: var(--bg-color);color: var(--text-color);padding:40px 20px;min-height:100vh}
        .container{max-width:800px;margin:0 auto}
        h1{text-align:center;margin-bottom:40px;font-size:48px}

        /* 顶部控制栏 */
        .top-bar{
            display:flex;flex-wrap:wrap;gap:12px;justify-content:center;margin-bottom:30px
        }
        .tab-btn{
            padding:10px 24px;border:none;border-radius:10px;font-size:18px;cursor:pointer;background:var(--card-bg);color:var(--text-color);border:1px solid var(--border-color);
        }
        .tab-btn.active{background:var(--primary);color:#fff;border-color:var(--primary)}

        /* 页面切换容器 */
        .page-front{display:block;}
        .page-admin{display:none;}
        .page-login{display:none;text-align:center;margin-top:100px;}

        /* 前台链接样式 */
        .link-group{margin-bottom:30px}
        .group-title{
            font-size:28px;margin-bottom:18px;padding-left:12px;
            border-left:6px solid var(--primary);line-height:1.2
        }
        .link-item{
            display:flex;align-items:center;justify-content:space-between;
            padding:24px 30px;background:var(--card-bg);border-radius:16px;
            box-shadow:0 2px 8px #00000008;
            margin-bottom:16px;font-size:32px;cursor:pointer;
        }
        .copy-btn{
            padding:10px 20px;background:var(--primary);color:#fff;border:none;
            border-radius:10px;font-size:20px;cursor:pointer;
        }
        .copy-btn:hover{filter:brightness(0.9)}

        /* 后台表单盒子 */
        .admin-box{
            background:var(--card-bg);padding:24px;border-radius:16px;margin-bottom:30px;box-shadow:0 2px 8px #00000008
        }
        .admin-box h3{font-size:24px;margin-bottom:16px}
        .input-item{margin-bottom:14px}
        .input-item label{display:block;font-size:18px;margin-bottom:6px;opacity:0.8}
        .input-item input, .input-item select{
            width:100%;padding:12px 16px;border:1px solid var(--border-color);border-radius:10px;font-size:18px;background:var(--card-bg);color:var(--text-color);
        }
        .submit-btn{
            width:100%;padding:14px;background:var(--primary);color:#fff;border:none;border-radius:10px;font-size:20px;cursor:pointer;margin-top:8px;
        }
        .del-btn{background:var(--danger)}

        /* 提示弹窗 */
        .toast{
            position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);
            background:rgba(0,0,0,0.75);color:#fff;padding:16px 32px;
            border-radius:12px;font-size:22px;display:none;z-index:9999
        }
        /* 手动复制弹窗 */
        .copy-fail-pop{
            position:fixed;inset:0;background:rgba(0,0,0,0.6);display:none;align-items:center;justify-content:center;z-index:9998;
        }
        .fail-inner{
            width:90%;max-width:500px;background:var(--card-bg);padding:24px;border-radius:16px;
        }
        .fail-textarea{
            width:100%;min-height:120px;padding:12px;font-size:18px;background:#fff;color:#000;
        }
        /* 编辑弹窗 */
        .edit-pop{
            position:fixed;inset:0;background:rgba(0,0,0,0.6);display:none;align-items:center;justify-content:center;z-index:9997;
        }
        .edit-inner{
            width:90%;max-width:500px;background:var(--card-bg);padding:24px;border-radius:16px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>常用链接汇总</h1>

        <!-- 顶部按钮组 -->
        <div class="top-bar">
            <button class="tab-btn active" id="btnFront">前台预览</button>
            <button class="tab-btn" id="btnAdmin">后台管理</button>
            <button class="tab-btn" id="themeToggle">切换暗黑模式</button>
            <button class="tab-btn" id="exportBtn">导出备份</button>
            <label class="tab-btn" style="cursor:pointer;">导入备份<input type="file" id="importFile" hidden accept=".json"></label>
        </div>

        <!-- 操作提示 -->
        <div class="toast" id="toast">操作成功！</div>

        <!-- 复制失败手动弹窗 -->
        <div class="copy-fail-pop" id="copyFailPop">
            <div class="fail-inner">
                <h3>自动复制失败，请手动复制</h3>
                <textarea class="fail-textarea" id="failUrlText" readonly></textarea>
                <p style="margin:10px 0;opacity:0.8;">长按文本 → 全选 → 复制</p>
                <button class="submit-btn" id="closeFailPop">关闭</button>
            </div>
        </div>

        <!-- 前台页面 -->
        <div class="page-front" id="pageFront">
            <div id="linkList"></div>
        </div>

        <!-- 后台登录页 -->
        <div class="page-login" id="pageLogin">
            <div class="admin-box" style="max-width:400px;margin:0 auto;">
                <h3>请输入后台密码</h3>
                <div class="input-item">
                    <input type="password" id="adminPwd" placeholder="默认密码：123456">
                </div>
                <button class="submit-btn" id="loginBtn">登录进入后台</button>
            </div>
        </div>

        <!-- 后台管理页 -->
        <div class="page-admin" id="pageAdmin">
            <!-- 添加分类 -->
            <div class="admin-box">
                <h3>新增分类</h3>
                <div class="input-item">
                    <label>分类名称</label>
                    <input type="text" id="newGroup" placeholder="例如：工作链接">
                </div>
                <button class="submit-btn" id="addGroupBtn">创建分类</button>
            </div>

            <!-- 添加链接 -->
            <div class="admin-box">
                <h3>新增链接</h3>
                <div class="input-item">
                    <label>选择分类</label>
                    <select id="selectGroup"></select>
                </div>
                <div class="input-item">
                    <label>链接名称</label>
                    <input type="text" id="linkName" placeholder="例如：百度">
                </div>
                <div class="input-item">
                    <label>链接地址</label>
                    <input type="text" id="linkUrl" placeholder="https://www.baidu.com">
                </div>
                <button class="submit-btn" id="addLinkBtn">添加链接</button>
            </div>

            <!-- 全部内容管理（编辑+删除） -->
            <div class="admin-box">
                <h3>链接与分类管理</h3>
                <div id="manageList"></div>
            </div>
        </div>

        <!-- 编辑弹窗 -->
        <div class="edit-pop" id="editPop">
            <div class="edit-inner">
                <h3>修改链接信息</h3>
                <div class="input-item">
                    <label>链接名称</label>
                    <input type="text" id="editName">
                </div>
                <div class="input-item">
                    <label>链接地址</label>
                    <input type="text" id="editUrl">
                </div>
                <input type="hidden" id="editGidx">
                <input type="hidden" id="editLidx">
                <button class="submit-btn" id="saveEdit">保存修改</button>
                <button class="submit-btn del-btn" id="closeEdit" style="margin-top:10px;">取消</button>
            </div>
        </div>
    </div>

<script>
// ========== 基础配置（修改后台密码在这里） ==========
const ADMIN_PASSWORD = "123456";
let linkData = JSON.parse(localStorage.getItem('linkData')) || [
    {
        groupName: "工作链接",
        links: [
            {name:"百度", url:"https://www.baidu.com"},
            {name:"链接名称1", url:"https://xxx.com"},
            {name:"链接名称2", url:"https://xxx2.com"}
        ]
    },
    {
        groupName: "娱乐链接",
        links: [
            {name:"B站", url:"https://bilibili.com"},
            {name:"链接名称3", url:"https://xxx3.com"}
        ]
    }
];

// DOM缓存
const toast = document.getElementById('toast');
const copyFailPop = document.getElementById('copyFailPop');
const failUrlText = document.getElementById('failUrlText');
const closeFailPop = document.getElementById('closeFailPop');
const pageFront = document.getElementById('pageFront');
const pageAdmin = document.getElementById('pageAdmin');
const pageLogin = document.getElementById('pageLogin');
const btnFront = document.getElementById('btnFront');
const btnAdmin = document.getElementById('btnAdmin');
const linkList = document.getElementById('linkList');
const manageList = document.getElementById('manageList');
const selectGroup = document.getElementById('selectGroup');
const editPop = document.getElementById('editPop');

// 关闭手动复制弹窗
closeFailPop.onclick = ()=> copyFailPop.style.display = 'none';

// 【MT专用兼容复制函数】
function copyLink(url) {
    // 动态创建textarea（安卓WebView最稳方案）
    const tempTextarea = document.createElement('textarea');
    tempTextarea.value = url;
    // 移出可视区域，不遮挡页面
    tempTextarea.style.position = 'fixed';
    tempTextarea.style.left = '-9999px';
    tempTextarea.style.top = '-9999px';
    tempTextarea.style.opacity = '0';
    document.body.appendChild(tempTextarea);

    // 全选文本
    tempTextarea.focus();
    tempTextarea.select();
    tempTextarea.setSelectionRange(0, url.length);

    let copySuccess = false;
    try {
        // 执行复制指令
        copySuccess = document.execCommand('copy');
    } catch (err) {
        copySuccess = false;
    }
    // 销毁临时元素
    document.body.removeChild(tempTextarea);

    if(copySuccess){
        showToast("链接复制成功！");
    }else{
        // 自动复制失效，弹出手动复制窗口
        failUrlText.value = url;
        copyFailPop.style.display = 'flex';
    }
}

// 轻提示
function showToast(msg="操作成功"){
    toast.innerText = msg;
    toast.style.display = 'block';
    setTimeout(()=>toast.style.display='none',2000);
}

// 保存本地数据
function saveData(){
    localStorage.setItem('linkData', JSON.stringify(linkData));
}

// 渲染前台页面
function renderFront(){
    let html = '';
    linkData.forEach(group=>{
        html += `<div class="link-group">
            <div class="group-title">${group.groupName}</div>`;
        group.links.forEach((item)=>{
            html += `<div class="link-item" data-url="${item.url}">
                <span>${item.name}</span>
                <button class="copy-btn" data-copy="${item.url}">复制链接</button>
            </div>`;
        })
        html += `</div>`;
    })
    linkList.innerHTML = html;

    // 卡片点击跳转
    document.querySelectorAll('.link-item').forEach(item=>{
        item.addEventListener('click',(e)=>{
            if(!e.target.classList.contains('copy-btn')){
                window.open(item.dataset.url,'_blank');
            }
        })
    })

    // 绑定复制按钮
    document.querySelectorAll('.copy-btn').forEach(btn=>{
        btn.onclick = function(e){
            e.stopPropagation();
            const url = this.dataset.copy;
            copyLink(url);
        }
    })
}

// 渲染后台分类下拉框
function renderAdminSelect(){
    let opt = '';
    linkData.forEach((g,idx)=>{
        opt += `<option value="${idx}">${g.groupName}</option>`
    })
    selectGroup.innerHTML = opt;
}

// 渲染管理列表
function renderManage(){
    let html = '';
    linkData.forEach((group,gIdx)=>{
        html += `<div style="padding:12px;border:1px solid var(--border-color);border-radius:10px;margin-bottom:12px;">
            <div style="font-size:20px;margin-bottom:8px;">分类：${group.groupName}
                <button class="submit-btn del-btn" onclick="delGroup(${gIdx})">删除整个分类</button>
            </div>`;
        group.links.forEach((link,lIdx)=>{
            html += `<div style="display:flex;flex-wrap:wrap;gap:6px;justify-content:space-between;align-items:center;padding:8px 0;border-top:1px solid var(--border-color);">
                <span style="max-width:60%;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;">${link.name}</span>
                <div>
                    <button class="submit-btn" style="width:auto;padding:6px 10px;font-size:14px;" onclick="openEdit(${gIdx},${lIdx})">编辑</button>
                    <button class="submit-btn del-btn" style="width:auto;padding:6px 10px;font-size:14px;" onclick="delLink(${gIdx},${lIdx})">删除</button>
                </div>
            </div>`
        })
        html += `</div>`
    })
    manageList.innerHTML = html;
}

// 删除分类
window.delGroup = function(gIdx){
    if(confirm('确定删除该分类及全部链接？')){
        linkData.splice(gIdx,1);
        saveData();refreshAll();
    }
}
// 删除单链接
window.delLink = function(gIdx,lIdx){
    linkData[gIdx].links.splice(lIdx,1);
    saveData();refreshAll();
}
// 打开编辑弹窗
window.openEdit = function(gIdx,lIdx){
    const item = linkData[gIdx].links[lIdx];
    document.getElementById('editName').value = item.name;
    document.getElementById('editUrl').value = item.url;
    document.getElementById('editGidx').value = gIdx;
    document.getElementById('editLidx').value = lIdx;
    editPop.style.display = 'flex';
}
// 关闭编辑弹窗
document.getElementById('closeEdit').onclick = ()=> editPop.style.display = 'none';
// 保存编辑
document.getElementById('saveEdit').onclick = function(){
    const gIdx = document.getElementById('editGidx').value;
    const lIdx = document.getElementById('editLidx').value;
    const newName = document.getElementById('editName').value.trim();
    const newUrl = document.getElementById('editUrl').value.trim();
    if(!newName||!newUrl) return showToast('内容不能为空');
    linkData[gIdx].links[lIdx] = {name:newName,url:newUrl};
    saveData();refreshAll();
    editPop.style.display = 'none';
    showToast('修改成功');
}

// 全局刷新
function refreshAll(){
    renderFront();
    renderAdminSelect();
    renderManage();
}

// 切换前台/后台
btnFront.onclick = ()=>{
    pageFront.style.display = 'block';
    pageAdmin.style.display = 'none';
    pageLogin.style.display = 'none';
    btnFront.classList.add('active');
    btnAdmin.classList.remove('active');
}
btnAdmin.onclick = ()=>{
    pageFront.style.display = 'none';
    pageAdmin.style.display = 'none';
    pageLogin.style.display = 'block';
    btnFront.classList.remove('active');
    btnAdmin.classList.add('active');
}

// 后台登录
document.getElementById('loginBtn').onclick = ()=>{
    const inputPwd = document.getElementById('adminPwd').value;
    if(inputPwd === ADMIN_PASSWORD){
        pageLogin.style.display = 'none';
        pageAdmin.style.display = 'block';
        refreshAll();
        showToast('登录成功');
    }else{
        showToast('密码错误');
    }
}

// 新增分类
document.getElementById('addGroupBtn').onclick = function(){
    const name = document.getElementById('newGroup').value.trim();
    if(!name) return showToast('请填写分类名称');
    linkData.push({groupName:name, links:[]});
    saveData();
    document.getElementById('newGroup').value = '';
    refreshAll();
    showToast('分类创建成功');
}

// 新增链接
document.getElementById('addLinkBtn').onclick = function(){
    const gIdx = selectGroup.value;
    const name = document.getElementById('linkName').value.trim();
    const url = document.getElementById('linkUrl').value.trim();
    if(!name || !url) return showToast('名称和链接不能为空');
    linkData[gIdx].links.push({name,url});
    saveData();
    document.getElementById('linkName').value = '';
    document.getElementById('linkUrl').value = '';
    refreshAll();
    showToast('链接添加成功');
}

// 明暗模式切换
const themeToggle = document.getElementById('themeToggle');
themeToggle.onclick = function(){
    const html = document.documentElement;
    if(html.getAttribute('data-theme') === 'dark'){
        html.removeAttribute('data-theme');
        this.innerText = '切换暗黑模式';
    }else{
        html.setAttribute('data-theme','dark');
        this.innerText = '切换浅色模式';
    }
}

// 导出备份
document.getElementById('exportBtn').onclick = function(){
    const blob = new Blob([JSON.stringify(linkData,null,2)],{type:'application/json'});
    const a = document.createElement('a');
    a.href = URL.createObjectURL(blob);
    a.download = '链接备份.json';
    a.click();
    showToast('备份文件已下载');
}

// 导入备份
document.getElementById('importFile').addEventListener('change',function(e){
    const file = e.target.files[0];
    if(!file)return;
    const reader = new FileReader();
    reader.onload = function(res){
        try{
            linkData = JSON.parse(res.target.result);
            saveData();
            refreshAll();
            showToast('数据导入成功');
        }catch(err){
            showToast('文件格式错误');
        }
    }
    reader.readAsText(file);
})

// 页面初始化
refreshAll();
</script>
</body>
</html>
