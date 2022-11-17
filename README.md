# lern-nodejs
lerning nodejs

## package.json example
````
{
   "name":"name1",
   "version":"0.0.1",
   "description":"",
   "author":"",
   "private":true,
   "license":"MIT",
   "scripts":{
      "prebuild":"rimraf dist",
      "build":"nest build",
      "format":"prettier --write \"src/**/*.ts\" \"test/**/*.ts\"",
      "start":"nest start",
      "run-serve":"ts-node src/main.ts",
      "run-mon":"yarn nodemon src/main.ts"
   },
   "dependencies":{
      "@nestjs-modules/mailer":"^1.6.0",
      "@nestjs/cli":"^7.5.3",
      "@nestjs/common":"^6.0.0",
      "@nestjs/config":"^0.5.0"
   }
}
````
