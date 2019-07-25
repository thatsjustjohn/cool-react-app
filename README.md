## yml 5
1st Error
Property validation failure: [Value of property {/DistributionConfig/Origins} does not match type {Array}]
change (~195)
        `Origins:
            DomainName: !GetAtt coolReactBucket.DomainName`
to this
       `Origins:
          -
            DomainName: !GetAtt coolReactBucket.DomainName`

2nd Error 
Pipeline should start with a stage that only contains source actions (Service: AWSCodePipeline; Status Code: 400; Error Code: InvalidStructureException; Request ID: 9f41dab8-7024-45c2-b267-1e881f376ce1)
Codepipline - stage - action that isn't 'source'
change (~32)
  `Stages:
        -
          Name: Source
          Actions:
            -
              Name: SourceAction
              ActionTypeId:
                Category: **Build**
                Owner: ThirdParty
                Provider: GitHub
                Version: 1`
to 
  `Stages:
        -
          Name: Source
          Actions:
            -
              Name: SourceAction
              ActionTypeId:
                Category: **Source**
                Owner: ThirdParty
                Provider: GitHub
                Version: 1`

3rd Error:
CREATE_COMPLETE.  But there are no fun things in my buckets!
we need to address the pipeline bucket
change(~135)
`                  - "s3:Object"
`
to
`                  - "s3:PutObject"
`

4th Error:
We have the zip in pipeline bucket but nothing in the cool react app
change(~174)
`- aws s3 cp --acl public-read ./build s3://${coolReactBucket}/
`
to
`- aws s3 cp --recursive --acl public-read ./build s3://${coolReactBucket}/
`



This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.<br>
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br>
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.<br>
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.<br>
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br>
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (Webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: https://facebook.github.io/create-react-app/docs/code-splitting

### Analyzing the Bundle Size

This section has moved here: https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size

### Making a Progressive Web App

This section has moved here: https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app

### Advanced Configuration

This section has moved here: https://facebook.github.io/create-react-app/docs/advanced-configuration

### Deployment

This section has moved here: https://facebook.github.io/create-react-app/docs/deployment

### `npm run build` fails to minify

This section has moved here: https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify
# cool-react-app
