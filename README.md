# Deploy Directus CMS on AWS Beanstalk

This is for deploying [Directus CMS](https://directus.io/) to AWS elastic beanstalk.

Create this repo because I saw a few people asking on the [Directus Discord](https://discord.gg/directus). This is an example repo for a beanstalk deployment. I would reccomend installing from the cli and not forking or cloning this repository.

## Directus Beanstalk Deploy:

1. In the package.json define the node engine and add the start command:

```json
{
  "scripts": {
    "start": "directus start"
    // ....more stuff here
  },
  "engines": {
    "node": ">=16.0.0"
  }
}
```

2. Update your .env to run on port localhost port 8080. (This is the default for Amazon Linux 2 nodejs)

```env
HOST=localhost
PORT=8080
```

3. Copy the files from the `.platform` directory in this folder into the root of your directus project. Then run the following commands:

```
chmod +x .platform/hooks/prebuild/00_npm_install.sh
chmod +x .platform/confighooks/prebuild/00_npm_install.sh
```

4. Thats it, you can now deploy on elastic beanstalk! 🚀

5. (Extra) Deploy on elastic beanstalk. Here's a few quick commands you can copy and paste to get it started from the cli:

```bash
eb create $(NAME_OF_ENVIROMENT) -i $(INSTANCE_TYPE)
```

***Note: I would reccomend using a bigger instance size because of the npm install command. If you try to use a micro instance, it may not install and error out. If you are using t3 size instance, t3.medium would be the minimum size I'd reccomend***

```
eb deploy
```
