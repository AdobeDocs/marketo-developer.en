---
title: User Profiles
feature: Mobile Marketing, Users and Roles
description: Using User Profiles in Marketo Mobile
exl-id: 1b2cfb7f-d678-4022-8cd9-a56004a1ac46
---
# User Profiles

How to Create User Profiles

1. [Creating User Profiles on iOS](#ios_user_profiles)
1. [Creating User Profiles on Android](#android_user_profiles)

## Creating User Profiles on iOS {#ios_user_profiles}

You can create rich profiles by sending the user fields as shown below.

```
MarketoLead *profile = [[MarketoLead alloc] init];

// Get user profile from network and populate
[profile setEmail:@"jd@makesomething.com"];
[profile setFirstName:@"John"];
[profile setLastName:@"Doe"];
[profile setAddress:@"1234KingFishSt"];
[profile setCity:@"SouthPadreIsland"];
[profile setState:@"CA"];
[profile setPostalCode:@"78596"];
[profile setCountry:@"USA"];
[profile setGender:@"male"];
[profile setLeadSource:@"_facebook_ads"];
[profile setBirthDay:@"01/01/1985"];
[profile setFacebookId:@"facebookid"];
[profile setFacebookProfileURL:@"facebook.com/profile"];
[profile setFacebookProfilePicURL:@"faceboook.com/profile/pic"];
[profile setLinkedInId:@"linkedinid"];
[profile setTwitterId:@"twitterid"];
```

```
let profile =  MarketoLead()

// Get user profile from network and populate
profile.setEmail("jd@makesomething.com")
profile.setFirstName("John")
profile.setLastName("Doe")
profile.setAddress("1234KingFishSt")
profile.setCity("SouthPadreIsland")
profile.setState("CA")
profile.setPostalCode("78596")
profile.setCountry("USA")
profile.setGender("male")
profile.setLeadSource("_facebook_ads")
profile.setBirthDay("01/01/1985")
profile.setFacebookId("facebookid")
profile.setFacebookProfileURL("facebook.com/profile")
profile.setFacebookProfilePicURL("faceboook.com/profile/pic")
profile.setLinkedInId("linkedinid")
profile.setTwitterId("twitterid")
```

Add more [standard fields](../rest-api/list-of-standard-fields.md).

>[!BEGINTABS]

>[!TAB Objective C]

```
// Add other custom fields
[profile setFieldName:@"mobilePhone"withValue:@"123.456.7890"];
[profile setFieldName:@"numberOfEmployees"withValue:@"10"];
[profile setFieldName:@"phone"withValue:@"123.456.7890"];
```

>[!TAB Swift]

```
// Add other custom fields
profile.setFieldName("mobilePhone" , withValue :"123.456.7890");
profile.setFieldName("numberOfEmployees", withValue: "10");
profile.setFieldName("phone", withValue:"123.456.7890");
```

>[!ENDTABS]

Report User Profile.

>[!BEGINTABS]

>[!TAB Objective C]

```
Marketo *sharedInstance = [Marketo sharedInstance];

// This method will update user profile
[sharedInstance associateLead:profile];
```

>[!TAB Swift]

```
let marketo = Marketo.sharedInstance()

// This method will update user profile
marketo.associateLead(profile)
```

>[!ENDTABS]

## Creating User Profiles on Android {#android_user_profiles}

1. Create User Profile.

    You can create rich profiles by sending user fields as shown below.

    ```java
    MarketoLead profile = new MarketoLead();

    // Get user profile from network and populate
    try {
        profile.setEmail("htcone3@gmail.com");
        profile.setFirstName("Mike");
        profile.setLastName("Gray");
        profile.setFacebookId("facebookid");
        profile.setAddress("1234 King Fish Blvd");
    }
    catch (MktoException e) {
        e.printStackTrace();
    }
    ```

1. Add more [standard fields](../rest-api/list-of-standard-fields.md).

    ```java
    // Add other custom fields
    profile.setCustomField("mobilePhone", "123.456.7890");
    profile.setCustomField("numberOfEmployees", "10");
    profile.setCustomField("phone", "123.456.7890");
    profile.setCustomField("rating", "R");
    profile.setCustomField("facebookDisplayName", "mini");
    profile.setCustomField("facebookReach", "10");
    profile.setCustomField("facebookReferredEnrollments", "100");
    profile.setCustomField("facebookReferredVisits", "9998");
    profile.setCustomField("lastReferredEnrollment", "03/01/2015");
    profile.setCustomField("lastReferredVisit", "03/01/2015");
    profile.setCustomField("linkedInDisplayName", "Android");
    ```

1. Report User Profile.

    ```java
    MarketoLead profile = new MarketoLead();

    // This method will update user profile
    marketoSdk.associateLead(profile);
    ```
