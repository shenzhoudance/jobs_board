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
resources :jobs
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

```
git checkout -b Gemfile_gem
https://rubygems.org/
gem 'haml', '~> 5.0', '>= 5.0.4'
gem 'bootstrap-sass', '~> 3.3', '>= 3.3.7'
gem 'simple_form', '~> 3.5', '>= 3.5.1'
bundle install
rails server
---
https://github.com/twbs/bootstrap-sass
app/assets/stylesheets/application.css.scss
---
@import "bootstrap-sprockets";
@import "bootstrap";
---
app/assets/javascripts/application.js
//= require bootstrap-sprockets
//= require turbolinks
---
https://github.com/plataformatec/simple_form
rails generate simple_form:install --bootstrap
---
app/views/jobs/index.html.haml
%h1 欢迎来到才华横溢的世界
rails server
```
![image](https://ws1.sinaimg.cn/large/006tKfTcgy1fpfluwiv4dj310y0eq0tm.jpg)
```
app/controllers/jobs_controller.rb
--
class JobsController < ApplicationController
 before_action :find_job, only: [:show,:edit,:update,:destroy]

 def index
   @job = Job.all.order("created_at DESC")
 end

 def show
 end

def new
  @job = Job.new
end

def create
  @job = Job.new(jobs_params)

  if @job.save
    redirect_to @job
  else
    render "New"
  end
end

 def edit
 end

 def update
 end

 def destroy
 end

 private

 def jobs_params
   params.require(:job).permit(:title, :description, :company, :url)
 end

 def find_job
   @job = Job.find(params[:id])
 end

end
---
```
