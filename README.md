# 才华横溢 jobs_board 案例教学 7

```
cd workspace
rails new jobs_board
cd jobs_board
git init
git status
git add .
git commit -m "initial commit "
git remote add origin https://github.com/shenzhoudance/jobs_board.git
git push -u origin master
```
```
atom .
rails server
http://localhost:3000/
```
![image](https://ws4.sinaimg.cn/large/006tKfTcgy1fpflfdsersj316q0xm4nx.jpg)
```
git checkout -b model_job
rails g model job title:string description:text company:string url:string
rake db:migrate
```
![image](https://ws3.sinaimg.cn/large/006tKfTcgy1fpflm7b1e4j31cq0judjv.jpg)
```
rails g controller jobs
config/routes.rb
---
resource :jobs
root 'jobs#index'
---
app/controllers/jobs_controller.rb
def index
end
---
app/views/jobs/index.html.erb
<h1>欢迎来到才华横溢的世界</h1>
---
```
![image](https://ws1.sinaimg.cn/large/006tKfTcgy1fpfluwiv4dj310y0eq0tm.jpg)
