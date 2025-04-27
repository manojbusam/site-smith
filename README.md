# Site Smith Project Setup

## 1. Configure Git Remote with SSH
```
# Change remote URL to SSH
git remote set-url origin git@github.com:manojbusam/site-smith.git

# Verify SSH connection
ssh -T git@github.com
# Expected response: "Hi manojbusam! You've successfully authenticated..."
```

## 2. Standard Git Workflow
```
# Stage changes
git add .

# Commit changes
git commit -m "Your descriptive message here"

# Push to main branch
git push origin main
```

## 3. Ansible Automation Setup
Create `ansible-setup/playbook.yml` with:
```
---
- hosts: localhost
  tasks:
    - name: Pull latest code
      git:
        repo: git@github.com:manojbusam/site-smith.git
        dest: ./site-smith
        version: main
        update: yes

    - name: Install React dependencies
      command: npm install
      args:
        chdir: ./site-smith/react-app

    - name: Start React app
      command: npm start
      args:
        chdir: ./site-smith/react-app
      async: 1000
      poll: 0
```

## 4. Run Ansible Playbook
```
ansible-playbook ansible-setup/playbook.yml
```

## 5. Manual React App Management
```
# Install dependencies
cd react-app && npm install

# Start development server
npm start
# Access at http://localhost:3000

# Create production build
npm run build
```

## Folder Structure
```
site-smith/
├── README.md
├── ansible-setup/
│   └── playbook.yml
└── react-app/
    ├── node_modules/
    ├── package.json
    └── src/
```
