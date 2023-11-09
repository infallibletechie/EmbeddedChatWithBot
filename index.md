<html>
<style type='text/css'>
	.embeddedServiceHelpButton .helpButton .uiButton {
		background-color: #005290;
		font-family: "Arial", sans-serif;
	}
	.embeddedServiceHelpButton .helpButton .uiButton:focus {
		outline: 1px solid #005290;
	}
</style>

<script type='text/javascript' src='https://service.force.com/embeddedservice/5.0/esw.min.js'></script>
<script type='text/javascript'>
	var initESW = function(gslbBaseURL) {
		embedded_svc.settings.displayHelpButton = true; //Or false
		embedded_svc.settings.language = ''; //For example, enter 'en' or 'en-US'
		embedded_svc.settings.enabledFeatures = ['LiveAgent'];
		embedded_svc.settings.entryFeature = 'LiveAgent';
		embedded_svc.settings.prepopulatedPrechatFields = {
		    FirstName: "Test",
		    LastName: "Test",
		    Email: "test@test.com",
		    Subject: "Testing"
		};
	
		window.addEventListener( "message", receiveMessage, false );

		function receiveMessage( event) {

			let payload = event.data;
			console.log(
				'Payload is',
				JSON.stringify( payload )
			);

			if ( payload && payload.type == 'CustomMessage' ) {
				
				console.log( 'Inside Post Message' );
				embedded_svc.postMessage( 
					"agent.sendMessage", 
					payload.message 
				);
	
			}

		};

		embedded_svc.addEventHandler( 
		    "onChatEndedByChasitor", 
		    function( data ) {
		    
		    console.log( 
		        'Chat was ended by the Visitor' 
		    );
		
		} );
		 
		embedded_svc.addEventHandler(
		    "onChatEndedByAgent", 
		    function( data ) {
		    
		    console.log( 
		        'Chat was ended by the Agent' 
		    );
		
		} );
		 
		embedded_svc.addEventHandler(
		    "onChatEndedByChatbot", 
		    function( data ) {
		
		    console.log( 
		        'Chat was ended by the BOT' 
		    );
		
		} );

		embedded_svc.init(
			'https://infallibletechie9-dev-ed.my.salesforce.com',
			'https://infallibletechie9-dev-ed.my.site.com/',
			gslbBaseURL,
			'00D5f000001yZYJ',
			'Embedded_Service_with_Bot',
			{
				baseLiveAgentContentURL: 'https://c.la4-c1-ia5.salesforceliveagent.com/content',
				deploymentId: '5725f000000TpP3',
				buttonId: '5735f000000Tpl7',
				baseLiveAgentURL: 'https://d.la4-c1-ia5.salesforceliveagent.com/chat',
				eswLiveAgentDevName: 'EmbeddedServiceLiveAgent_Parent04I5f000000PKfzEAG_17c600abedf',
				isOfflineSupportEnabled: false
			}
		);
	};

	if (!window.embedded_svc) {
		var s = document.createElement('script');
		s.setAttribute('src', 'https://infallibletechie9-dev-ed.my.salesforce.com/embeddedservice/5.0/esw.min.js');
		s.onload = function() {
			initESW(null);
		};
		document.body.appendChild(s);
	} else {
		initESW('https://service.force.com');
	}
</script>
</html>
