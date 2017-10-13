---
layout: post
title:  "Slow builds and fast deploys"
date:   2017-07-20 20:13:53 +0200
categories: development
---

What would you think if your <a href="https://en.wikipedia.org/wiki/Software_developer">developers</a> have to wait for a long time before trying the code changes that they have just coded? I remember 5 years ago a project that the <a href="https://en.wikipedia.org/wiki/Software_build">build</a> and <a href="https://en.wikipedia.org/wiki/Software_deployment">deploy</a> of the application spent <b>13 minutes</b> and <b>21 seconds</b>. That's <b>801 seconds</b>. (I wrote it in my diary that's why I remember it)  

Time wasted
------------------

If you multiply this time by the number of deploys per day that a developer can do that's, 801 seconds * n deploys = 801n seconds = <b>0.2225n hours</b> per day. If you multiply (considering 20 days of work by month for 12 months) 0.2225n * 20 days * 12 months = <b>53.4n hours</b> per year that are wasted because of an slow build process which is <b>6.675*n unproductive days</b> per year for this developer.

![Number of days wasted]({{ site.baseurl }}/images/plot.png)

If n=15 then the number of days wasted per year is 100 :O (100/(20*12) -> <b>41%</b> of work days in a year)

We are not considering other factors that decrease the productivity of the developer that during this time that he is waiting, he starts doing other tasks losing the <a href="https://www.youtube.com/watch?v=77RubAueWjg">focus</a> on what he was doing.  

Add the hourly pay rate that you pay to your developers and that's some money.

{% highlight python %}

6.675 *
n *
num_devs_in_company *
hourly_pay_rate = 
money = 
time

{% endhighlight %}

All this leads me to think that in a big organization it's important to concienciate everybody, a team or at least one person to check what improvements can be made in order to speed up the build and deployment processes. All this time could be dedicated to implement new products or services that could bring value to your organization. This is what is called the <a href="http://www.investopedia.com/terms/o/opportunitycost.asp">cost of opportunity</a> and it applies to your work life and also to your personal life.

If the build spends a lot of time possibly it's because you have to compile a lot of code and if you have a lot of code maybe you have a big application that should be split into smaller pieces to reduce the build time and create microservices.


Saving time 
----------------

All that saves time, is something good. It's impossible to reduce the time of build to 0 seconds but keeping your build and deploy fast should be something to consider while you have a team of developers.

In my team I have to develop software in different software modules and we try to keep it simple and fast to build and deploy. One thing that we did was to create a maven profile that everytime a clean install is done locally, it copies the ear automatically to the deployment folder of the JBoss using the `JBOSS_HOME` environment variable and using the <a href="http://maven.apache.org/plugins/maven-antrun-plugin/">maven-antrun-plugin</a>

{% highlight xml %}

        <profile>
            <id>deploy-jboss-64</id>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <executions>
                            <execution>
                                <id>deploy-DU</id>
                                <phase>install</phase>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                                <configuration>
                                    <tasks>
                                        <copy overwrite="true" file="target/${project.artifactId}.ear"
                                              todir="${env.JBOSS_HOME}/standalone/deployments"/>
                                    </tasks>
                                </configuration>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>  

{% endhighlight %}

This saves time to me (and to the other developers that develop in the same module) everytime that I have to deploy a new version of an <a href="https://en.wikipedia.org/wiki/EAR_(file_format)">ear</a> file in my local JBoss. Otherwise I had to manually copy the ear resulting from the build into the deployments folder of the JBoss. 


[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
