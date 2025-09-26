# Git 명령어

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global --list
git config pull.rebase true  # 다른 커밋과 충돌 시 merge해서 올림
```

### 깃 여러 커밋 정리 방법
1. `git rebase -i HEAD~<커밋개수>`
2. vi 창에서 맨 위는 `pick`, 나머지는 `squash` 로 변경
3. `git push --force`
4. 잘못된 경우: `git rebase --abort`
5. 마지막에 origin에 풀리퀘할 때 없는 커밋이 있으면 풀리퀘 안 됨 → 브랜치 새로 파서 변경점 반영

### Git SSH 키 생성 방법 (권한 추가)
```bash
ssh-keygen -t rsa -C "soohwan.cho"
```
- `~/.ssh` 폴더에 `id_rsa.pub` 파일 생성
- 해당 내용을 Git 웹 페이지의 **Add Key**에 **Read/Write** 권한으로 추가

### 자주 쓰는 명령어 모음
- 전체 내용 업데이트: `git remote update` (= `git fetch --all`)
- 브랜치 체크아웃: `git checkout -b <branch_name>`
- 브랜치 업데이트(fetch): `git fetch`
- Push: `git push`
- 최초 Push: `git push origin master`
- Pull(Fetch + Merge): `git pull`
- 변경사항 스테이징: `git add <file>`
- 변경사항 모두 스테이징: `git add .`
- Commit: `git commit -m "Commit message"`
- 상태 확인: `git status`
- 모든 원격/로컬 브랜치 표시: `git branch -a`
- 브랜치 트리 표시: `git show-branch`

---

# tmux 명령어

- 실행 중인 세션 목록: `tmux list-session` (= `tmux ls`)
- 새 세션: `tmux new -s 'session_name'`
- 세션 연결: `tmux attach -t 'session_name'`
- 현재 세션 종료: `exit`
- 특정 세션 종료: `tmux kill-session -t <session_name>`
- 모든 세션 종료: `tmux kill-server`
- 세션 탈출(세션 유지): `Ctrl+b, d`

### 창 관련
- 새 창 생성: `Ctrl+b, c`
- 창 목록 보기: `Ctrl+b, w`
- 다음/이전 창 이동: `Ctrl+b, n` / `Ctrl+b, p`
- 특정 창 이동: `Ctrl+b <window_no>`
- 현재 창 닫기: `Ctrl+b &`

### 패널 분할 및 전환
- 가로 분할: `Ctrl+b "`
- 세로 분할: `Ctrl+b %`
- Pane 간 전환: `Ctrl+b o`
- Pane 이동: `Ctrl+b + [화살표]`
- 현재 Pane 닫기: `Ctrl+b x`

---

# 리눅스 명령어

### 패키지 관리
```bash
sudo apt update
sudo apt-get update
```

### SSH 원격 접속
```bash
ssh -p 49184 shcho@163.152.124.58   # L40s
ssh -p 49184 shcho@163.152.124.82   # Poseidon
ssh -p 49184 shcho@163.152.124.89   # Cat
```

### SSH 원격 파일 전송
```bash
scp -P 49184 C:\Users\windows10\Downloads\kaggle.json \
    shcho@163.152.124.82:~/.config/kaggle/
```

### 파일/디렉터리 관리
- 디렉터리 삭제: `rm -r <dir>` (recursive)
- tar 압축 풀기: `tar -xvzf <tar_file>`

### GPU 선택 실행
```bash
CUDA_VISIBLE_DEVICES=1 python script.py
```
(= 1번 GPU만 사용)

---

# ✨ 추가 팁
- **git log 보기**: `git log --oneline --graph --decorate --all`
- **브랜치 삭제**: `git branch -d <branch>` (로컬), `git push origin --delete <branch>` (원격)
- **tmux 세션 이름 변경**: `Ctrl+b $`
- **리눅스 디스크 사용량 확인**: `du -sh *` (현재 폴더별 용량 요약), `df -h` (전체 디스크 용량)
- **백그라운드 실행**: `nohup python script.py &`
- **프로세스 확인**: `htop` 또는 `ps aux | grep python`

