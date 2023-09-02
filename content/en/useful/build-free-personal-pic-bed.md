---
title: "Build Personal Pic-Bed, Free"
date: 2022-08-08T21:00:00+08:00
tags: ["free","tools","workflows","github","cdn","pic-bed"]
toc: true
tocNum: false
---


## Requirements Analysis

- Usage scenarios

We often need to add images to our articles (notes, essays, blogs, etc.). Taking the common **Markdown** editor **Typora** note-taking scenario as an example, if we copy and paste the image directly into it, we will get the following result:

![](https://gcore.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-pic-bed-example-001-changed.jpeg)

You can see that the link representing the image is its local relative path, which leads to the following disadvantages:

- Articles are difficult to migrate, for instance,if they are posted on the Internet in the form of blogs, **images will not load correctly**
-  does not guarantee data security if **only storage locally**
- due to **Git**'s feature, if image resources are stored locally, it is difficult to use it to version important articles which have a large number of images

With a Pic-Bed, the image link will be as follows, in the form of an absolute path stored on the Internet

```url
https://gcore.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-pic-bed-example-001-changed.jpeg
```

This makes it easy to store only the link of the image on the server in the articles. Content migration and version management become easy

## Solution Comparison

There are multiple options for building Pic-beds. Here is an analysis of the pros and cons of two common methods to support the superiority of our technology selection

| methods                                                 | Pros                             | Cons                                                                                                             |
| ------------------------------------------------------- | -------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| Pic-bed providers such as Qiniu Cloud, SM.MS and others | Easy to operate and usually fast | Paid, risk of bankruptcy, data autonomy, limited speed and capacity of the free version, and difficult migration |
| self-built Pic-bed on a server                          | Data is secure and autonomous    | The operation is relatively cumbersome and there is a personal server cost                                       | 

## Technical Selection

- Use **<a href="https://github.com/" target="_blank">GitHub</a>**  repository as a free Pic-bed (please use resources wisely, don't waste them)
- Free CDN service using **<a href="https://www.jsdelivr.com/" target="_blank">jsDelivr</a>** (guarantee high-speed access to repository resources)
- Simplify operations with the automatic upload service provided by **<a href="https://picgo.github.io/PicGo-Doc/en/" target="_blank">PicGo</a>**

The advantages of this set of solutions are: **completely free**, fast speed, easy operation, pictures can be stored locally and in the cloud at the same time, and data is self-secure

## Concrete Implementation

### Pre-knowledge

1. Basic usages of <a href="https://git-scm.com/" target="_blank">Git</a> and GitHub

### Step-by-step Instructions

1. Create a **public** repository on GitHub to use as a free Pic-bed

**Notice:** It must be a public repository, otherwise you cannot take advantage of the automatic upload service provided by **PicGo**

2. Generate `token`: 
    - On the **GitHub** personal account page: `Settings` --> `Developer settings`
    - --> `Personal access tokens` --> `Generate new token` 
    - --> `Expiration` select `no expiration` --> `Select scopes` Check `repo` 
    - --> `Generate token` --> Make a note of the generated `token`

> GitHub interface corresponding to the relevant operation
![](https://gcore.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-pic-bed-example-002.png)

3. Download **<a href="https://picgo.github.io/PicGo-Doc/en/" target="_blank">PicGo</a>** and open **Pic-Bed Settings** page:
    1. Open the GitHub Pic-Bed page, set as **Default Pic-Bed**
    2. Set the repository name to `username/repo_name` (replace it with your own GitHub username/repository name you created in step 1)
    3. Set the branch name to `main` (or `master`)
    4. Set the token to the token generated in the previous step
    5. Specify the storage path e.g. `img/`
    6. Set a custom domain `https://gcore.jsdelivr.net/gh/username/repo_name`

> the Pic-Bed Settings page
![](https://gcore.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-pic-bed-example-003.png)

4. Enable the automatic upload service

Configure automatic upload service in your own editor such as **Typora** In the settings page, image --> Image Upload Setting, set Image Uploader to **PicGo**, in addition, it is highly recommended to use the <a href="https://obsidian.md/" target="_blank">Obsidian</a> editor, which can be used with plugins for the best experience. Please <a href="https://google.com" target="_blank">search</a> for other editors' configurations yourself.
    
> obsidiain Image auto upload plugin interface
![](https://gcore.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-pic-bed-example-004.png)

5. Complete, have a test and enjoy using your own picture bed~

> after configuring pic-bed in Typora, paste a image to it and it will appear a Upload Image option, click it
![](https://gcore.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-pic-bed-example-005.png)

We can find these images in our own GitHub repository,

> image uploaded to the GitHub repository (attention!) <mark>Loading images directly in GitHub requires VPN if you are in China</mark>, and that's why we use custom links to use CDN service)
![](https://gcore.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-pic-bed-example-006.png)

You can also pull them to local storage with the command `git pull` to ensure your own data security.

Enter commands in terminal to pull the images to local computer
![](https://gcore.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-pic-bed-example-007.png)

> image files that are stored locally
![](https://gcore.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-pic-bed-example-008.png)

The following image is the image uploaded to the picture bed in the example:

![](https://gcore.jsdelivr.net/gh/AlexLiu2022/resources/img/Ophelia.JPG)

Its source code in the blog is:
```
![](https://gcore.jsdelivr.net/gh/AlexLiu2022/resources/img/Ophelia.JPG)
```

<style>
h1.post-title.p-name {
  margin-top: 0 !important;
}
</style>