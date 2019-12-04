---
title: 清除 Git Commits
date: 2019-12-04 15:33:55
categories: 
- Git
tags:
- Git
- Commit
---

```
# Clone your git repo
git clone https://github.com/xxx.git;
# Entre your local repo
cd xxx;
# Checkout
git checkout --orphan latest_branch;
# Add all the files
git add -A;
# Commit the changes
git commit -am "Reinitialize";
# Delete the branch
git branch -D master;
# Rename the current branch to master
git branch -m master;
# Finally, force update your repository
git push -f origin master;
```

转载自：https://blog.csdn.net/yolohohohoho/article/details/90607229
