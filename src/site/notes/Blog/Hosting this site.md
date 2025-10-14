---
{"dg-publish":true,"permalink":"/blog/hosting-this-site/","title":"GitHub Pages"}
---

# Hosting this site

## TLDR
[[Blog/Hosting this site#Success\|Hosting this site#Success]]

## References
- https://dev.to/defenderofbasic/host-your-obsidian-notebook-on-github-pages-for-free-8l1
- https://github.com/barkstone2/vault-to-blog
- https://notes.nicolevanderhoeven.com/How+to+publish+Obsidian+notes+with+Quartz+on+GitHub+Pages
- https://github.com/oleeskild/Obsidian-Digital-Garden?tab=readme-ov-file
- https://github.com/foxblock/digitalgarden_gh-pages
- 

## Discussion
As I've been figuring out how to migrate from my Samsung Android phone running [One UI](https://en.wikipedia.org/wiki/One_UI) to the [Pixel 9 Pro XL](https://en.wikipedia.org/wiki/Pixel_9) I bought and on which I've installed [GrapheneOS](https://grapheneos.org/), I've wished for more guides on how to accomplish certain tasks. The [GrapheneOS Discussion Board](https://discuss.grapheneos.org/) has been very helpful, but I don't always know what I don't know. So when I realized that this was an achievable goal I decided to try to document my journey in a way that I could publish online for other folks. 

I'm not really a blogger, so I didn't want to pay a monthly fee for this one website. I eventually found [GitHub Pages](https://docs.github.com/en/pages), which looked like just what I wanted. I then started looking at methods to ***easily*** publish my notes there. I wanted to be able to adjust the "how-to" notes I normally take so that they'd make sense to somebody other than me, then easily just export those notes to GitHub Pages.

At first I'd settled on [[Notes/Joplin\|Joplin]], as I liked it's simplicity and full [FOSS](https://en.wikipedia.org/wiki/Free_and_open-source_software) nature. I still like Joplin as a note-taking app. I tried three different "publish to GitHub Pages" plugins:
- [Joplin Publisher](https://joplin-utils.rxliuli.com/en-US/joplin-publisher/)
- [Pages Publisher](https://github.com/ylc395/joplin-plugin-pages-publisher)
- And one I can't remember the name

All three worked, but they were intended to publish blog posts, not a website like this one. So I ended up having to switch to [[Notes/Obsidian\|Obsidian]]. I ***like*** Obsidian.md, but it's not really FOSS. However, I need to be able to focus on updating the pages' content and not on the process of publishing, and Obsidian was able to offer that to me. Though it took a LOT of trouble to figure out how to get it to work.

## First Failure
[This](https://dev.to/defenderofbasic/host-your-obsidian-notebook-on-github-pages-for-free-8l1) process looked relatively easy. Once I figured out the missing step the author had omitted it worked very well. For one day. Then I started getting an unformatted XML page whose contents looked like they were the Table of Contents tab to the left of the site. Despite deleting the repository and starting the entire process over again, I was unable to get the site to come back up. So I tried a different route.

## Second Try
Next I tried [vault-to-blog](https://github.com/barkstone2/vault-to-blog). I installed it from the community plugins, but when I tried to save the URL for the local repository on my Windows PC, I got the following error: "Failed to remove remote. Error: Git.cwd: cannot change to non-directory `"C:\Users|<redacted>\Documents\Obsidian\DeGoogle/.obsidian/plugins/vault-to-blog/react-app/0.0.6/react-app".` Sure enough, I couldn't find 'react-app' int the 'plugins' directory, and Googling for a solution was fruitless. (Yes, I am fully aware of the irony in using Google to search for tools to get rid of Google.)

Then I found this page: https://github.com/barkstone2/vault-to-blog/issues/160, and I realized that I'd tried to create my GitHub page as a non-main repository. When I deleted everything and started over, I was able to get it working. Unfortunately I wasn't able to figure out how to set up a homepage. I tried a page at the base of the directory named "README", and another named "index", and neither would show up by default when I brought up the website. So I continued looking. The process worked, but didn't look the way I wanted and I didn't want to spend the time figuring out how to modify the site.

## Third Try
I next tried [Fork My Brain's solution](https://notes.nicolevanderhoeven.com/How+to+publish+Obsidian+notes+with+Quartz+on+GitHub+Pages). I'd seen it earlier, but I'd been attempting to avoid installing yet more dependencies on my Windows computer (in this case JodeJS and NPM). Also, NPM has had some [security nightmares](https://www.cisa.gov/news-events/alerts/2025/09/23/widespread-supply-chain-compromise-impacting-npm-ecosystem) lately, but I ***really*** wanted to stop spending so much time on this publication route.  

As with everything I'd tried so far (with the exception of vault-to-blog), I was able to get it to work one time and then it stopped updating. By this time I was so frustrated that I didn't even try to figure out how to get it to update.

## Fourth Try
I finally found the [Digital Garden](https://obsidian.md/plugins?search=digital%20garden) plugin which I  got working. However, I didn't like that while I was pushing the notes to Github, the [Digital Garden ] were then being published to Vercel with a weird URL. 

## Success
I finally found a fork of the [Digital Garden](https://github.com/oleeskild/digitalgarden) github repository called [digitalgarden_gh-pages](https://github.com/foxblock/digitalgarden_gh-pages) by foxblock. It works with the [Digital Garden](https://obsidian.md/plugins?search=digital%20garden) plugin but publishes to my GitHub Pages. I won't go through the installation process, the one on the [digitalgarden_gh-pages](https://github.com/foxblock/digitalgarden_gh-pages) site are very clear. However, I will note one thing because it took me awhile to find it.

I wanted the file tree on the left of the site so people could find individual pages easily. It's not there by default. To get it to display, go into the plugin settings and click on "manage note settings". Then turn on the "show filetree sidebar" toggle.

> [!note]+ I'm sure many of you are asking "why, if you were having so much trouble, didn't you just use [Obsidian Publish](https://obsidian.md/publish)?" I seriously considered it.  But as much as I'd like to support the Obsidian project, $96/year for a website I'm only using to share my self-hosting setup is a bit much. If I was a blogger or if I had more to share on a regular basis, I'd definitely have gone with OP.



