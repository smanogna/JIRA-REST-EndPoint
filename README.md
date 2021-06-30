# JIRA-REST-EndPoint

import com.onresolve.scriptrunner.runner.rest.common.CustomEndpointDelegate
import groovy.json.JsonBuilder
import groovy.transform.BaseScript

import javax.ws.rs.core.MultivaluedMap
import javax.ws.rs.core.Response
import com.atlassian.jira.component.ComponentAccessor
import com.atlassian.jira.user.util.UserUtil
import com.atlassian.jira.security.groups.GroupManager
import com.atlassian.jira.security.JiraAuthenticationContext

@BaseScript CustomEndpointDelegate delegate

getagentcount(httpMethod: "GET") { MultivaluedMap queryParams, String body ->
    UserUtil userUtil = ComponentAccessor.getUserUtil()
	long acount = 0
	acount = ComponentAccessor.groupManager.getUsersInGroup("service-desk-agents", false).size();
    return Response.ok(new JsonBuilder([LicenseCount: acount]).toString()).build();
}
