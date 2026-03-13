# Meeting Notes

Liviu Moron 11:08 AM Hello

Nicolas Waern 11:16 AM https://winniioio-my.sharepoint.com/:p:/g/personal/ceo\_winniio\_io/IQCEcrASEZLCRbKjUnzZFdQfAUBpSoaDYrAEJlm7tZIsjfM?e=UWTujO

Nicolas Waern 11:19 AM This was some of the stuff I've been working on 2-3 years ago that I'm still using to frame conversations etc.

I have worked a lot with energy aspects as well, grid flexibility, smart energy systems, smart heating systems.

Not super interested in technical interoperability, but more other interoperability dimensions higher up in the interoperability taxonomy, semantic, syntactic, organizational, legal, contextual, social, etc etc related to reality - where spatial anchoring in inspire and and across time is usually what I use to anchor interoperability discussions in space and time.

Nicolas Waern 11:20 AM Regarding this, have you discussed A2A agentic communication, MCP aspects, etc? And the opportunities and challenges? As well as going from LLMs to LQMs? 11:21 AM Not in this WG , at least not yet

Nicolas Waern 11:21 AM ok

Nicolas Waern 11:22 AM I would say the mimimal interoperability mechanism is to have a map, the map of the world as the boundary spanning object to anchor this, with outcomes as the primary objective, and then compare how outcomes were achieved, what capabilities were used, what requirements where needed, and then be able to compare outcomes with completely different recipes. 11:24 AM Nicolas, could you contribute this here? https://forms.gle/b8idRe27yUcgZex17

Nicolas Waern 11:38 AM Basing it in physics - is somewhat future proof :)

Bjorn Hagstrom 11:41 AM I do not think C3 is minimal any more. It should be out of scope for the MIM now. It could be a recommendation but not a requirement but there is no room for that in the MIMs.

Gert Hilgers 11:42 AM Olaf-Gerd: agreed on the standards comment; but then the question also is how we define "minimal". Either way, this is a conversation worth having

Gert Hilgers 11:46 AM Nicolas: for non-technical interoperability considerations, in particular organisational, you may be interested in working group 7 at the U4SSC thematic group on digital transformation for people-centred cities: policy and practice of organizational interoperability. https://u4ssc.itu.int/digital-transformation/

Nicolas Waern 11:48 AM I was obsessing a bit about AI PMs right now. In the tools that a PM can bring with them, claude md files, or a backpack of AI agents that do different things etc etc.

Maybe we could create something around this. a tool box, trusted, exaplainable, asepcts... that could be packaged for a mayor as a capability...package? 11:49 AM I am hearing importance of xAI, Trusted Mechanisms for AI data sharing, how do we capture this? Exactly my thoughts Nicolas

Nicolas Waern 11:50 AM Just brainstorming on my own here. But, doing that based on EU taxonomy, interoperability perspective might be useful. So that they get a document and move through it with the MIMS perspecrives and the EU taxonomy for interoperability dimensions spanning technical, semantic, syntactic, dimensions and to see if/how these are addressed, and it would provide a trust score, not limiting or prohibiting outcomes to be created

Gert Hilgers 11:50 AM AI-orchestrated PM is an exciting topic I am also spending quit a bit of time on. This is (currently) outside the scope of OASC, though.

Nicolas Waern 11:51 AM Yes, but we might be able to bring it back so that it's "grounded" in some principles, rules, guidelines, that do exist.

Nicolas Waern 11:52 AM So that a municipality 1 can,, say we achieved these outcomes. With 86% transparency score, so now we can go back and increase it.

Or municipality 2 says, we achieved better outcomes for the same problem, but we only have 46% trust score/explainability score - let's unpack it looking at x dimensions

Gert Hilgers 11:52 AM That's how it has to be done, agreed.

Nicolas Waern 11:54 AM This is the way I have spoken 11:54 AM :)

Nicolas Waern 11:54 AM (rewatching mandalorian...)

Bjorn Hagstrom 11:54 AM :) 11:56 AM Should C3 than be more about how we can "extract" semantics or a data model from serialized data? https://csvw.org/

Gert Hilgers 12:00 PM Back in a moment

Nicolas Waern 12:01 PM Have to jump! Let's make the world interoperable (again?)! 12:01 PM Thx Nicolas!

Bjorn Hagstrom 12:10 PM My si My suggestion for C1 so it is clear: "C1: All entities included in data sources are described using consistent data models" 12:13 PM Any coordinate system should also make explicit its Coordinate Reference System (CRS) in order to allow you to transform them. This is a part of the OGC standards, but not always explicit in GeoJSON

Anders Gavler 12:14 PM I as well have to sneak out.

My two cents are if not C1 and C2 handles C3 (as I think Björn indicated) it should be kept since I think the capability is at the core of the principles that a city should work towards and all cities are not mature and they need guidance in this.

If it is easly solved using AI - which was my interpretation of the discussion - all the better since then it should be easy to use existing and coming standards to harmonize the requirement and mechanism levels towards these standards or bcp:s and make it understandeble for cities and municipalities.

See ya! 12:14 PM https://alikucukafor flowsvci.github.io/FSO/

Bjorn Hagstrom 12:15 PM Last time I looked Geojson have to use a certain reference system according to the standard (cant remember the name now). So if you do not want to convert you have to not use GeoJson or to cheat.

Bjorn Hagstrom 12:19 PM Concerning validation: A city should validate that their data delivery complies with standards. This could be a requirement I think. A good guidance outside of the MIMs can help cities think about how to do this.

Bjorn Hagstrom 12:25 PM Ah WGS84 is ofc the referens system you need to use in GeoJson and no city in Sweden uses that

Khalfi el mehdi 12:25 PM https://ontop-vkg.org/tutorial/basic/university-1.html#ontology-classes-and-properties

Bjorn Hagstrom 12:25 PM An not in europe I would guess either.
