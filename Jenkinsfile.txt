pipeline
{
agent any

tools
{
jdk 'JDK17'
maven 'myMaven'
}

stages
{

stage('Checkout')
{
steps 
{
git 'https://github.com/meenukalai/spring-petclinic-devops.git'
}
}

stage('Build')
{
steps
{
bat 'mvn clean package'
}
}

stage('Test')
{
steps
{
bat 'mvn test'
}
 stage('Build Docker Image')
{
steps
{
bat 'docker build -t petclinic:v1 .'
}
stage('Run Container')
{
steps
{
bat 'docker run -itd --name myc3 -p 8080:8080 petclinic:v1'
}
stage('push Docker Image')
{
steps
{
bat 'docker push meenukalai/petclinic:v1'
}
}
}

}
}
