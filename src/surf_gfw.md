# The Great Firewall of China 墙

> 2025-04-02

## 0. 墙内备用链接
### 0.1. 墙内访问GitHub
- GitHub(镜像站点1): [https://bgithub.xyz](https://bgithub.xyz)  
- GitHub(镜像站点2): [https://ggithub.xyz](https://ggithub.xyz)
### 墙内访问Hugging Face
- Hugging Face(镜像站点): [https://hf-mirror.com/](https://hf-mirror.com/)

## 1. 编程语言墙内镜像站点
### 1.1. Python
- pip: [https://mirrors.ustc.edu.cn/help/pypi.html](https://mirrors.ustc.edu.cn/help/pypi.html) 
- conda: [https://mirrors.ustc.edu.cn/help/anaconda.html](https://mirrors.ustc.edu.cn/help/anaconda.html)

### 1.2. Rust
- rustup tool chains: [https://mirrors.ustc.edu.cn/help/rust-static.html](https://mirrors.ustc.edu.cn/help/rust-static.html)
- cargo crates: [https://mirrors.ustc.edu.cn/help/crates.io-index.html](https://mirrors.ustc.edu.cn/help/crates.io-index.html)

## 2. Shell Proxy 
- Pwsh
  ```pwsh
  $env:ALL_PROXY="http://127.0.0.1:16888"
  ```
- bash
  ```bash
  export ALL_PROXY="http://127.0.0.1:16888"
  ```