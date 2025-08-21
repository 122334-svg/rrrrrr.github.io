配置：
python3.10+
RDKit

首先，创建一个专用的pyhton环境
`conda create -n smile2d3d python=3.10 -y`
`conda activate rdkitenv`
安装必要库
`conda install -c rdkit rdkit -y`
`pip install flask flask-cors`


### 代码实现

首先，导入必要库
`from flask import Flask, request, Response`
`from rdkit import Chem`
`from rdkit.Chem import AllChem`
`from flask_cors import CORS`

Flask, request, Response：Flask 框架的核心组件，用于创建 Web 应用、处理请求和生成响应
rdkit.Chem, rdkit.Chem.AllChem：RDKit 库的化学信息处理模块，用于分子结构处理
flask_cors.CORS：处理跨域资源共享（CORS），允许不同域名的前端调用该 API

应用初始化
`app = Flask(__name__)`
`CORS(app)`
启用CORS，解决跨域请求问题，确保前端可以从不同域名访问该服务

定义API端点
`@app.route("/sdf", methods=["POST"])`

核心函数
```
def generate_sdf():
    # 获取输入数据
    data = request.get_json()
    smiles = data.get("smiles", "")

    #验证并解析 SMILES
    #使用 RDKit 的MolFromSmiles方法将 SMILES 字符串转换为分子对象
    mol = Chem.MolFromSmiles(smiles)
    if not mol:
        return Response("Invalid SMILES", status=400)

    #分子结构处理
    mol = Chem.AddHs(mol) # 加氢
    AllChem.EmbedMolecule(mol, AllChem.ETKDG()) # 核心函数-生成分子的3D构象
    AllChem.UFFOptimizeMolecule(mol) # 使用UFF力场优化分子结构

    #生成并返回 SDF
    sdf = Chem.MolToMolBlock(mol)
    # 保存到服务器并生成对应路径的sdf文件
    save_dir = "/users/ruishi/ligand"。#服务器里面路径
    os.makedirs(save_dir, exist_ok=True)
    timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
    filename = f"{save_dir}/mol_{timestamp}.sdf"
    with open(filename, "w") as f:
        f.write(sdf)

    return Response(sdf, mimetype="chemical/x-mdl-sdfile")

```

运行应用
```
if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```
当脚本直接运行时，启动 Flask 开发服务器，监听所有网络接口（0.0.0.0）的 5000 端口

请求指令
```
curl -X POST http://localhost:5000/sdf \
  -H "Content-Type: application/json" \
  -d '{"smiles": "CCO"}' 
```
这个localhost表示服务运行在你当前电脑上
端口5000为默认端口
这个CCO是举例乙醇的smile码

> 引用学习自[SanyaShresta25](https://github.com/SanyaShresta25/titration-tracker-backend/commits?author=SanyaShresta25) 