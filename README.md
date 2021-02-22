<h1>jenkins lazy....</h1>
<h3>Jenkins in k8s</h3>
<p>Create jenkins pod with 8080 and 50000 services exposed using svc type LoadBalancer</p>

<pre><code>kubectl apply -f jenkins.yaml
</code></pre>

<h3>Jenkins in Docker</h3>
<p>Create a docker container that has privileges to use the host machine's docker.sock. With this setup jenkins container is able to create new containers for CI/CD operations</p>
<p>Always check if jenkins user exists on host machine first, if so add it to the group docker</p>
<pre><code>#add group if it does not exist
#groupadd -g 999 docker
cat /etc/groups | grep -i docker
usermod -aG docker jenkins
</code></pre>

<p>Start jenkins container
<pre><code>docker run -p 8080:8080 -p 50000:50000 -v /var/jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock --name jenkins -d jenkins-docker:latest</code></pre>
