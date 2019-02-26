# rails get stalled because of spring

DISABLE_SPRING=1 rails generate devise:install

To check if the problem comes from spring :
spring stop
rails generate

# kill a rails server

lsof -wni tcp:3000

# Make a gem for the 1st time

https://www.sodifrance.fr/blog/creer-et-publier-une-gem-ruby/
@pblayo on rubygems.org
