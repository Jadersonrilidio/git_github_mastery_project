# Alura Git & GitHub Basic Course

description

---

## 1. Creating github account

TODO:

---

## 2. Creating a github repo

TODO:

---

## 3. Installing git on local machine

```bash
sudo apt install git
```

---

## 4. Git init command

```bash
git status  # if fatal error, means there is no git project versioning yet 
git init    # creates a .git file and start tracking/versioning your project
```

---

## 5. Git vs github explanation

TODO:

---

## 6. Sincronizing repos

```bash
touch README.md
echo "# Alura Git Github Basic Course" >> README.md
git init
git config --global user.email "user@email.com"
git config --global user.name "Username"
git add .
git commit -m "first commit"
git branch -M master
git remote add origin git@github.com:user/repo
git push -u origin master
```

---

## 7. SSH keys

```bash
ssh-keygen -t ed25519 -C "user@email.com"
```

---

## 8. Git remote commands

git remote add <name> <url>
git remote remove <name> 
git remote set-url <name> <new_url>
git remote rename <name> <new_name>

**Examples:**

```bash
git remote --help                                           # open git remote manual to read
git remote                                                  # list all remote repos in your project
git remote -v                                               # list all remote repos in your project (more verbose)
git remote add origin git@github.com:user/repo              # add a remote repo to your project
git remote remove origin                                    # remove a remote repository from your project
git remote set-url origin https://github.com/user/repo.git  # alter your project's remote origin repo URL to pull/push/fetch
git remote rename origin new-origin                         # rename a remote repository localy
```

---

## 9. Token-based authentication on github

TODO:

(link)[https://www.alura.com.br/artigos/nova-exigencia-do-git-de-autenticacao-por-token-o-que-e-o-que-devo-fazer]

---

## 10. Cloning a repo 

```bash
git clone https://github.com/user/repo.git 
```

---

## 11. Commits

```bash
git status
git add README.md                   # or `git add .` to add all unstaged files
git restore --staged README.md      # to unstagge a specific stagged file
git restore --staged .              # to unstagge all staged files
git commit -m "commit message"      # commit staged files with a message (-m)
git log                             # commit logs, with hash, branches involved, author, date and message if any - also shows the HEAD and current commit status of remote branches
git log --oneline                   # reduced one line commit logs
```

**commit messages tips**
As mensagens dos commits devem ser simples e objetivas. A seguir, listamos algumas orientações para isso:

    - Mantenha a mensagem curta e concisa: A primeira linha da mensagem deve conter, no máximo, 72 caracteres. Caso seja necessário uma descrição adicional, você deve pular uma linha e adicionar os detalhes, como o contexto, da mudança realizada.
    - Uso de verbo no infinitivo: É comum que a mensagem do commit inicie com um verbo no infinitivo que descreva a alteração feita, como “adicionar”, “corrigir” ou “atualizar”. Em sequência, são adicionados detalhes concisos da mudança. Por exemplo: “Atualizar texto do título da página”.
    - Evite detalhes técnicos: Não inclua detalhes técnicos complexos na mensagem de commit. Esses detalhes podem ser adicionados nos comentários de código ou na documentação.

É importante ter em mente que a mensagem do commit é uma forma de documentação do histórico das mudanças que ocorreram ao longo do código. A pessoa que ler essa mensagem pode não ter conhecimento do contexto original. Assim, garanta que suas mensagens de commit tenham clareza e sejam suficientemente descritivas.

**when to make a commit**
Um commit deve ser realizado sempre que você finalizar uma tarefa específica ou resolver algum bug. Isso mantém o histórico de commits claro e rastreável, de modo que seja possível entender o que foi feito em cada commit.

Assim, é importante realizar commits frequentemente. Porém, evite realizar commits muito pequenos ou muito grandes, pois isso pode tornar difícil o seu entendimento.

Lembre-se de nunca realizar um commit de um código que você sabe que contém bugs. O ideal é que o commit contenha somente código funcional.

**How git control changes**
O controle de mudanças do Git é feito através dos commits. Cada commit armazena o estado completo do projeto em um determinado momento por meio de um **snapshot**. Ou seja, cada commit é um registro completo do repositório no momento em que esse commit foi criado.

Como cada commit é uma representação completa e consistente do estado do projeto em um determinado ponto no tempo, isso facilita a rastreabilidade e o entendimento de como se deu a evolução do código ao longo do tempo.

Todo commit conta com um id único e traz uma referência aos commits anteriores. Assim, através dessa cadeia de commits, o Git registra um histórico completo de todos os commits realizados no repositório.

Caso queira conhecer melhor sobre esse processo, acesse a (documentação oficial do Git)[https://git-scm.com/book/pt-br/v2/Come%C3%A7ando-O-B%C3%A1sico-do-Git].

---

## 12. Push commits

```bash
git push -u origin master   # for the first commit, use `-u` to set the default stream to pull/push from
git push origin master
```

**adding another accounts to collaborate with your project**

Invitation:
    on github repo >> settings >> collaborators >> add people >> (add username, full name or email) >> invite

Collaborator:
    on email >> find invitation mail >> accept invite >> done
    on github >> ?

**Adding more commit co-authors**

```bash
$ git commit -m "add new feature.
>
>
Co-authored-by: NOME <nome@email.com>
Co-authored-by: OUTRO-NOME <outro@email.com>"
```

---

## 13. Git pull commands

```bash
git pull origin master      # pull all commits made from the remote origin master branch to your current branch 
git log                     # to check if the pulled source is on HEAD with the last 'master' repo 
```

---

## 14. Git integration on VSCode

TODO:

---

## 15. Handling versioning conflicts


```bash
# First, alter and make a commit on the same line remotely on github site `"\n old info"`
echo "\n new info" >> README.md
git add .
git commit -m "message"

git pull origin master # or git push origin master?

> remote: Enumerating objects: 5, done.
> remote: Counting objects: 100% (5/5), done.
> remote: Compressing objects: 100% (3/3), done.
> remote: Total 3 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
> Unpacking objects: 100% (3/3), 972 bytes | 486.00 KiB/s, done.
> From github.com:Jadersonrilidio/git_github_mastery_project
>  * branch            master     -> FETCH_HEAD
>    300e415..db34f68  master     -> origin/master
> hint: You have divergent branches and need to specify how to reconcile them.
> hint: You can do so by running one of the following commands sometime before
> hint: your next pull:
> hint: 
> hint:   git config pull.rebase false  # merge
> hint:   git config pull.rebase true   # rebase
> hint:   git config pull.ff only       # fast-forward only
> hint: 
> hint: You can replace "git config" with "git config --global" to set a default
> hint: preference for all repositories. You can also pass --rebase, --no-rebase,
> hint: or --ff-only on the command line to override the configured default per
> hint: invocation.
> fatal: Need to specify how to reconcile divergent branches.
```

### ChatGPT conflict resolution manner:

**Step 0 — Inspect before acting (recommended)**

```bash
git status
git log --oneline --graph --decorate --all
dit diff        # https://git-scm.com/docs/git-diff/pt_BR
```

This helps you see: how many local commits you have - how many remote commits exist - where branches diverged

**Option 1 — MERGE (safe, explicit history)**

When to use: Team projects - You don’t want to rewrite history - You’re okay with a merge commit

```bash
git pull --no-rebase origin master
```

Result: Creates a merge commit - Preserves full branch history - No commits are rewritten

**Option 2 — REBASE (clean, linear history) ⭐ popular choice**

When to use: Personal projects - Feature branches - You want a clean history

```bash
git pull --rebase origin master
# if conflicts appear
git add .
git rebase --continue
# abort if needed
git rebase --abort
```

What Git does: Temporarily removes your local commits - Updates your branch from origin/master - Reapplies your commits on top

**Option 3 — FAST-FORWARD ONLY (strict mode)**

When to use: You want Git to refuse merges - You want to keep history ultra-clean

```bash
git pull --ff-only origin master
```

Result: Works only if no divergence exists - Otherwise, Git aborts

**BEST OPTION — Correct way in team projects (recommended)**

```bash
git pull --no-rebase origin master
# Git will stop and say:
CONFLICT (content): Merge conflict in README.md
# Open the conflicted file, you will see something like:
<<<<<<< HEAD
checking how conflicts are handled with git/github
=======
testing conflicts handling on git/github
>>>>>>> origin/master
# Explicitly choose YOUR version - Edit the file to (remove the conflict markers):
checking how conflicts are handled with git/github
# Save and close.
git add README.md
git commit
# Git will create a merge commit that says:
# “We had a conflict, and THIS is the correct final version.”
git push origin master
```

---

## 16. Undoing commits - git revert

git revert <commit_id>
git revert -n <target_commit_hash>

```bash
git log
git revert 5e89699efc695cc122f1f0f2b5cbaeaffa33683f             # revert a commit, creating a new commit over
git revert -n 5e89699efc695cc122f1f0f2b5cbaeaffa33683f          # revert a commit, creating a new commit over
git revert --no-edit 5e89699efc695cc122f1f0f2b5cbaeaffa33683f   # skip the Nano commit message editor opening
git commit                                                      # to apply the reversion made previously
```

---

## 17. Undoing commits - git reset

git reset --hard <commit_id>

```bash
git reset --hard 33359d3265b5b5ba7c080773533493293882f5c1   # reset your local repository to the 
git push --force origin master                              # force the remote repository to reset all commits above (not recommended)
git push --force-with-lease origin master                   # This prevents overwriting remote work if someone pushed new commits that you don't have locally. This is the professional safe way.
```

It is worth to say that the `git reset` is viable only when you're undoing commits on your local repo, when working within team projects the most interesting is to use `git revert` or another options, in accordance with the team 

**Chat-GPT: git reset options**

Understanding Git’s 3 layers:

    1. HEAD (last commit snapshot)
    2. Staging Area (index)
    3. Working Directory (your files on disk)

`git reset` moves the branch pointer, but flags (--soft, --mixed, --hard) determines what happens to the other layers.


1. git reset --soft <commit_id>
    ✅ Moves HEAD
    ❌ Does NOT change staging area
    ❌ Does NOT change working directory

Effect:
    Your commit disappear
    Changes remains stagged

Uses:
    Squashing commits
    Rewriting commit messages
    Reorganizing commits cleanly


2. git reset --mixed <commit_id> (DEFAULT)
    ✅ Moves HEAD
    ✅ Resets staging area
    ❌ Does NOT change working directory

Effect:
    Your commit disappear
    Changes goes unstagged

Uses:
    Uncommit but keep changes
    Rework a commit from scratch


3. git reset --hard <commit_id>
    ✅ Moves HEAD
    ✅ Resets staging area
    ✅ Resets working directory

Effect:
    Your commit disappear
    All changes dissapear
    Files revert to target commit snapshot

If you didn’t push, you can recover using `git reflog`, but it feels like deletion.

Uses:
    Dangerous
    Use when working in projects alone


**Professional Rule of Thumb**
🔹 use `reset`
    On local branches
    Before pushing
    When cleaning history
    When working alone

🔹 use `revert`
    On shared branches
    After pushing
    On production branches
    When traceability matters


---

## 18. Altering commits - git commit --amend [options]

```bash
git commit --amend                                      # add newly stagged or modified files
git commit --amend -m "altering last commit's message"  # add newly stagged or modified files and rewrite commit message
```

---

## 19.

TODO:

---

## 20.

TODO:

---

## 21. Extra Content

### Make a basic git-github workflow for group project collaboration

```bash
# From your local master branch:

git log --oneline               # to check whether your current master branch (or anothers) is up to comparing to the remote master (and other ones)
git pull origin master          # to stay update with the project remote repo
# could be used other commands to handle conflict, as FETCH / MERGE / REBASE / etc
git status                      # to check your modifications, staged and unstaged files
git add .                       # to add all modifications or add only specific files with `git add <filenames>`
git commit -m "message"         # to ...
git push origin master          # to push your commit directly to the remote master repo
git push origin author-branch   # to push your commit to a specific branch on the remote repo

```

---

### Step-by-step: How to collaborate with open source projects on GitHub - Best Practices Guide


---

###


---


<!------------------------------------------------------------------------
Annotations:

Finished windows:
    https://git-scm.com/book/pt-br/v2/Come%C3%A7ando-O-B%C3%A1sico-do-Git
    https://www.alura.com.br/artigos/open-source-uma-breve-introducao
    https://git-scm.com/docs/git-diff/pt_BR
    https://git-scm.com/docs/git-reset
    https://www.conventionalcommits.org/en/v1.0.0-beta.4/

------------------------------------------------------------------------->