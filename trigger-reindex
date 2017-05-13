$ErrorActionPreference = "Stop"
$jiraURL = "jira.yourdomain.com"
$restapiuri = "https://$jiraURL/rest/api/2/reindex?type=BACKGROUND"
$recipients = "jonh.smith@yourdomain.com>"

$user = "username"
$pass = "password"
$pair = "$($user):$($pass)"
$encodedCreds = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($pair))
$basicAuthValue = "Basic $encodedCreds"
$Headers = @{
    Authorization = $basicAuthValue
}

$output = ""
try 
{
      $output += "JIRA INDEXING TRIGGERED `n`n"
      $jsonresponse = Invoke-WebRequest -URI $restapiuri -ContentType "application/json" -Method POST -Headers $Headers  -v
      $output += $jsonresponse
}
catch
{
      $output += "`n`n"
      $output += $_.Exception.Message
}

send-mailmessage -from "JIRA Indexing <someemail@yourdomain.com>" -to $recipients -subject "JIRA Indexing" -body $output -priority High -dno onSuccess, onFailure -smtpServer exchange.yourdomain.com
