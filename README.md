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

- rake routes

```
app/controllers/jobs_controller.rb
---
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
   if @job.update(jobs_params)
     redirect_to @job
   else
     render "Edit"
 end
end

 def destroy
   @job.destroy
   redirect_to root_path
 end


 private

 def jobs_params
   params.require(:job).permit(:title, :description, :company, :url)
 end

 def find_job
   @job = Job.find(params[:id])
 end

end
```
```
app/views/jobs/_form.html.haml
---
= simple_form_for(@job,html:{class:'form-horizontal'}) do |f|
  = f.input :title,label:"job title"
  = f.input :description,label:"job title"
  = f.input :company,label:"job company"
  = f.input :url,label:"link to job"
  %br/
  = f.button :submit
---
app/views/jobs/index.html.haml
%h1 欢迎来到才华横溢的世界

- @job.each do |job|
  %h2= link_to job.title,job
  %p= job.company


= link_to "new job",new_job_path
---
app/views/jobs/new.html.haml
---
%h1 New Job

= render 'form'

= link_to "Back", root_path, class: "btn btn-default"
---
app/views/jobs/edit.html.haml
---
%h1 Edit Job

= render 'form'

= link_to "Back", root_path
---
app/views/jobs/show.html.haml
---
%h1= @job.title
%p= @job.description
%p= @job.company

= link_to "home",root_path
= link_to "edit",edit_job_path(@job)
= link_to "delete",job_path(@job),method: :delete, data: { confirm: "are you sure?"}

```
![image](https://ws4.sinaimg.cn/large/006tKfTcgy1fpfupu2twmj30yw0gy3zo.jpg)
![image](https://ws4.sinaimg.cn/large/006tKfTcgy1fpfuovfa8uj30ua0v23zz.jpg)
![image](https://ws3.sinaimg.cn/large/006tKfTcgy1fpfup5rl63j30t20suta6.jpg)
![image](https://ws3.sinaimg.cn/large/006tKfTcgy1fpfupkpcpwj30jq0cct94.jpg)

```
git checkout -b category
rails g categary name:string
rake db:migrate
rails g migration add_category_id_to_jobs category_id:integer
rake db:migrate
```
![image](https://ws3.sinaimg.cn/large/006tKfTcgy1fpfuuefydqj31ei0lg78l.jpg)

```
app/models/job.rb
---
class Job < ApplicationRecord
  belongs_to :category
end

app/models/category.rb
---
class Category < ApplicationRecord
  has_many :jobs
end
```
```
rails c
Category
Category.connection
Category.create(name: "Full Time")
Category.create(name: "Part Time")
Category.create(name: "Freelance")
Category.create(name: "Consulting")
Category.all
job
Job
reload！
@job = Job.last
@job = Job.find(1)
exit
---
```
![image](https://ws1.sinaimg.cn/large/006tKfTcgy1fpfvpjt3d3j31420jsahg.jpg)
![image](https://ws2.sinaimg.cn/large/006tKfTcgy1fpfvpa1h36j315c0s4doc.jpg)
![image](https://ws4.sinaimg.cn/large/006tKfTcgy1fpfvp039n6j315s0ratfu.jpg)
![image](https://ws2.sinaimg.cn/large/006tKfTcgy1fpfvprnyw2j31dc0vagnk.jpg)


```
# 最后效果图：

![image](https://ws3.sinaimg.cn/large/006tKfTcgy1fpfxzgtbevj31kw0ndgx1.jpg)
