# Containers

## Setup the project

* Create [new github repo](https://github.com/new): ![](../.gitbook/assets/create-github-repo-for-project.png)
* Clone repo:

  ```text
  git clone https://github.com/denseidel/consumer-marketplace-service.git
  cd consumer-marketplace-service
  git secrets --install
  git secrets --register-aws
  ```

* Start a virtual environment

  ```text
  virtualenv venv --python=python3
  source venv/bin/activate
  # install pylint 
  pip install pylint
  ```

  If you use visual studio code do this first in your terminal window and then open the folder again with `code .`.

## Developer a docker microservice in Python

1. Check that you have have a local docker environment in [Plattform](../plattform.md) -&gt; Setup Docker Environment.
2. Create Dockerfile and docker-compose that starts the Mock Server\([Code](https://github.com/denseidel/products-marketplace-service/commit/6303f0ba152be610dc4fabcf85d624a4e32faa31)\) - make sure the Swagger  file does not include custom functions like `x-tokenInfoFunc`. **TODO create it for the mock** 
   * [Environment Variables to connect to AWS](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html)
3. Implement Frontend against mocks
4. Update Dockerfile to production config
5. Implement API \(including DB, ...\)

Connexion Examples:

* [https://github.com/hjacobs/connexion-example](https://github.com/hjacobs/connexion-example)
* [https://github.com/ssola/python-flask-microservice](https://github.com/ssola/python-flask-microservice)
* [http://blog.bejanalex.com/2017/03/mongodb-rest-api-interface-in-docker/](http://blog.bejanalex.com/2017/03/mongodb-rest-api-interface-in-docker/)

Create a client library for the API:

* [https://realpython.com/blog/python/api-integration-in-python/](https://realpython.com/blog/python/api-integration-in-python/)

Use Feature flags:

* [https://featureflags.io/python-feature-flags/](https://featureflags.io/python-feature-flags/)

Python Testing:

* Unit Testing
* Mocks
* Code Coverage

Python Functional Programming:

* [https://maryrosecook.com/blog/post/a-practical-introduction-to-functional-programming](https://maryrosecook.com/blog/post/a-practical-introduction-to-functional-programming)

Python Clean Code:

* [http://pythonforengineers.com/writing-great-code/](http://pythonforengineers.com/writing-great-code/)
* [https://github.com/zedr/clean-code-python](https://github.com/zedr/clean-code-python)
* [https://github.com/rmariano/Clean-code-in-Python/blob/master/build/Clean code in Python.pdf](https://github.com/rmariano/Clean-code-in-Python/blob/master/build/Clean%20code%20in%20Python.pdf)
* [http://docs.python-guide.org/en/latest/writing/reading/](http://docs.python-guide.org/en/latest/writing/reading/)



Benefits API First:

![](../.gitbook/assets/advantages-of-api-first.png)

[https://github.com/swagger-api/swagger-codegen/wiki/server-stub-generator-howto\#python-flask-connexion](https://github.com/swagger-api/swagger-codegen/wiki/server-stub-generator-howto#python-flask-connexion)

[http://connexion.readthedocs.io/en/latest/cli.html](http://connexion.readthedocs.io/en/latest/cli.html)

[https://blog.runscope.com/posts/openapi-swagger-resource-list-for-api-developers](https://blog.runscope.com/posts/openapi-swagger-resource-list-for-api-developers)

[https://medium.com/ibm-data-science-experience/deploy-your-python-functions-as-a-rest-api-811981ec7ec5](https://medium.com/ibm-data-science-experience/deploy-your-python-functions-as-a-rest-api-811981ec7ec5)

[https://github.com/zalando/connexion](https://github.com/zalando/connexion)

[http://michal.karzynski.pl/blog/2016/06/19/building-beautiful-restful-apis-using-flask-swagger-ui-flask-restplus/](http://michal.karzynski.pl/blog/2016/06/19/building-beautiful-restful-apis-using-flask-swagger-ui-flask-restplus/)

[https://cidrblock.github.io/zero-to-api-in-4-minutes.html](https://cidrblock.github.io/zero-to-api-in-4-minutes.html)

Beispiel: [https://github.com/hjacobs/connexion-example](https://github.com/hjacobs/connexion-example)

### Develop API First in Python

Get started with Connextion: [http://connexion.readthedocs.io/en/latest/quickstart.html](http://connexion.readthedocs.io/en/latest/quickstart.html)

[https://github.com/zalando/connexion](https://github.com/zalando/connexion)

[https://github.com/hjacobs/connexion-example](https://github.com/hjacobs/connexion-example)

[https://cidrblock.github.io/zero-to-api-in-4-minutes.html](https://cidrblock.github.io/zero-to-api-in-4-minutes.html)

[https://github.com/ssola/python-flask-microservice/blob/master/api/room.py](https://github.com/ssola/python-flask-microservice/blob/master/api/room.py)

[https://medium.com/@ssola/building-microservices-with-python-part-i-5240a8dcc2fb](https://medium.com/@ssola/building-microservices-with-python-part-i-5240a8dcc2fb)

[http://coderobot.downley.net/swagger-driven-testing-in-python.html](http://coderobot.downley.net/swagger-driven-testing-in-python.html)

[https://uwsgi-docs.readthedocs.io/en/latest/](https://uwsgi-docs.readthedocs.io/en/latest/)

[http://connexion.readthedocs.io/en/latest/routing.html](http://connexion.readthedocs.io/en/latest/routing.html)

* [https://medium.com/@ssola/building-microservices-with-python-part-i-5240a8dcc2fb](https://medium.com/@ssola/building-microservices-with-python-part-i-5240a8dcc2fb)
* [https://github.com/hjacobs/connexion-example/blob/master/app.py](https://github.com/hjacobs/connexion-example/blob/master/app.py)
* [http://connexion.readthedocs.io/en/latest/request.html](http://connexion.readthedocs.io/en/latest/request.html)
* Check a token: [https://auth0.com/docs/api-auth/tutorials/verify-access-token](https://auth0.com/docs/api-auth/tutorials/verify-access-token)

API Sources / public api collection: [https://any-api.com](https://any-api.com)

[https://www.programmableweb.com/apis/directory](https://www.programmableweb.com/apis/directory)

[https://apis.guru/browse-apis/](https://apis.guru/browse-apis/)

