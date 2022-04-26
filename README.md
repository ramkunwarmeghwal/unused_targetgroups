# unused_targetgroups

import boto3
import pprint
#boto3.setup_default_session(profile_name='staging/prod/test')

client = boto3.client('elbv2')

tn = []
target_arn = []
load_arn = []

tg = client.describe_target_groups(PageSize=400)
for i in tg['TargetGroups']:
    #pprint.pprint(i)
    tn.append(i['TargetGroupName'])
    target_arn.append(i['TargetGroupArn'])
    load_arn.append(i['LoadBalancerArns'])


lbs = elb.describe_load_balancers(PageSize=400)

ids=[]

for lb in target_arn:
    
    
    inss=elb.describe_target_health(TargetGroupArn=lb)
    
    instanceids=[]
    for ins in inss["TargetHealthDescriptions"]:        
        
        if (ins['Target']['Id'])==[]:
            instanceids.append([])

        else:
            instanceids.append(ins['Target']['Id'])

    ids.append(instanceids)
    #print(ids)
    
l = []
for i in ids:
    l.append(i)
    

#pprint.pprint(list(zip(tn,l)))
    
l1 = []
for i in list(zip(tn,l)):
    if i[1]==[]:
        l1.append(i[0])
        

pprint.pprint(l1)
