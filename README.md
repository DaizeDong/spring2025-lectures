# Spring 2025 CS336 lectures

This repo contains the lecture materials for "Stanford CS336: Language modeling from scratch".

## Non-executable (ppt/pdf) lectures

Located in `nonexecutable/`as PDFs

## Executable lectures

Located as `lecture_*.py` in the root directory

You can compile a lecture by running:

        python execute.py -m lecture_01

which generates a `var/traces/lecture_01.json` and caches any images as
appropriate.

However, if you want to run it on the cluster, you can do:

        ./remote_execute.sh lecture_01

which copies the files to our slurm cluster, runs it there, and copies the
results back. You have to setup the appropriate environment and tweak some
configs to make this work (these instructions are not complete).

### Frontend

If you need to tweak the Javascript:

Install (one-time):

        npm create vite@latest trace-viewer -- --template react
        cd trace-viewer
        npm install

Load a local server to view at `http://localhost:5173?trace=var/traces/sample.json`:

        npm run dev

Deploy to the main website:

        cd trace-viewer
        npm run build
        git add dist/assets
        # then commit to the repo and it should show up on the website

### 本地运行

```powershell
# 0) 安装 Node.js
winget install OpenJS.NodeJS.LTS --source winget

# 1) 先确认有编译产物
python execute.py -m lecture_01  # 生成 var/traces/lecture_01.json

# 2) 把 JSON 复制到前端的 public（会被静态托管）
mkdir -Force trace-viewer/public/var/traces
Copy-Item var/traces/lecture_01.json trace-viewer/public/var/traces/

# 3) 起 dev server
cd trace-viewer
$env:Path += ";C:\Program Files\nodejs"
npm run dev

# 4) 浏览器打开（注意前导 /）
# http://localhost:5173/?trace=/var/traces/lecture_01.json
```