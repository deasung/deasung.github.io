---

title: SpringBoot AWS Email 모듈 만들기
published: true
comments : true
---


AWS SES(Simple Email Service) 이메일 송수신용 

예전에 만들었지만 에버노트 정리도 할꼄 포스팅을 한다 

```java
import com.amazonaws.AmazonClientException;
import com.amazonaws.auth.profile.ProfileCredentialsProvider;
import com.amazonaws.services.simpleemail.AmazonSimpleEmailService;
import com.amazonaws.services.simpleemail.AmazonSimpleEmailServiceClientBuilder;
import com.test.config.property.AwsSesProperty;
import com.test.model.AwsSesEmailSender;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Slf4j
@Service
public class AwsEmailSenderService {

    @Autowired
    private AwsSesProperty awsSesProperty;

    public void send(AwsSesEmailSender senderDto){
        try {
            log.info("Attempting to send an email through Amazon SES by using the AWS SDK for Java...");

//            ProfileCredentialsProvider credentialsProvider = new ProfileCredentialsProvider();
//
//
//            try {
//                credentialsProvider.getCredentials();
//            } catch (Exception e) {
//                throw new AmazonClientException(
//                        "Cannot load the credentials from the credential profiles file. " +
//                                "Please make sure that your credentials file is at the correct " +
//                                "location (~/.aws/credentials), and is in valid format.",
//                        e);
//            }

//            AmazonSimpleEmailService client = AmazonSimpleEmailServiceClientBuilder.standard()
//                    .withCredentials(credentialsProvider)
//                    .withRegion("us-west-2")
//                    .build();

            AmazonSimpleEmailService client = awsSesProperty.amazonSimpleEmailService();


            // Send the email.
            client.sendEmail(senderDto.toSendRequestDto());
            log.info("Email sent! " + senderDto.toString() );

        } catch (Exception ex) {
            log.error("The email was not sent.");
            log.error("Error message: " + ex.getMessage());
            throw new AmazonClientException(
                    ex.getMessage(),
                    ex);
        }
    }


}
```

Gradle에 이렇게 추가를 해준다 


```gradle
//2018.05.28 aws ses 라이브러리 추가
compile('com.amazonaws:aws-java-sdk-ses:1.11.227’)
```


```
package com.test.config.property;

import com.amazonaws.ClientConfiguration;
import com.amazonaws.auth.AWSCredentials;
import com.amazonaws.auth.BasicAWSCredentials;
import com.amazonaws.regions.Region;
import com.amazonaws.regions.Regions;
import com.amazonaws.services.simpleemail.AmazonSimpleEmailService;
import com.amazonaws.services.simpleemail.AmazonSimpleEmailServiceClient;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

/**
 * AWS 이메일 서비스용 빈
 */
@Configuration
public class AwsSesProperty {

    @Value("${cloud.aws.credentials.accessKey}")
    private String accessKey;

    @Value("${cloud.aws.credentials.secretKey}")
    private String secretKey;

    @Bean
    public AmazonSimpleEmailService amazonSimpleEmailService() {
        AWSCredentials credentials = new BasicAWSCredentials(accessKey, secretKey);
        ClientConfiguration configuration = new ClientConfiguration();
        configuration.setConnectionTimeout(3000);
        AmazonSimpleEmailService client = new AmazonSimpleEmailServiceClient(credentials);
        client.setRegion(Region.getRegion(Regions.US_WEST_2));
        return client;
    }

}
```

실제 컨트롤단에서는 

```
Context context = new Context();
context.setVariable("user",user);
String html = templateEngine.process("email/email-template", context);

List<String> to = new ArrayList<>();
to.add(user.getEmail());

AwsSesEmailSender awsSesEmailSender = new AwsSesEmailSender(EAMIL_SENDER,to,EMAIL_PASSWORD_REQUEST_SUBJECT,html);

new Thread() {
    public void run() {
        awsEmailSenderService.send(awsSesEmailSender);
    }

}.start();

```