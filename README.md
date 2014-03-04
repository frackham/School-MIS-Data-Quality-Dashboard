School-MIS-Data-Quality-Dashboard
=================================

#Markdown test area for mobile clients.

#H1 Test
##H2 Test
###H3 Test
####H4 Test
#####H5 Test
######H6 Test
#######H7 Test

This is standard body text, except for *this* really **bold** bit.

But as Deming said:

>In God we trust, everyone else bring data.

Maybe that looks better as a code block?

```
In God we trust, everyone else bring data.
```

And here's a code block for vba:

```vb
option explicit
public function DoDemoVBACode() as string()
  dim sLang as string
  sLang = "VBA" #Don't judge me.
  msgbox("Well, here's some demo code. It's in the " & sLang & " language.") 
end function
```


#Principles

1. **Open source**. Both development and the app itself is open source. I (we?) feel like this is too imporrtant to lave to MIS vendors. Ideally this'd be a open source language as well, but that'll probably intergere with...
2. **Simple to deploy and setup**. If there's not formal support, it's gotta be easy. As in unzip a folder easy.
3. **Easily exten_dable_**. Got a new rule to test? Just add it to your schedule, and let the dashboard discover it.
4. **Real, actionable measurement**.
5. **Tweak and adapt to your school _over time_, not at deployment**.
6. **Easily exten_sible_**. [See here for the difference between extendable and extensible]().

< This one's a bit geeky. Sorry.

7. **Assessment last**. Assessment is arguably the most powerful of the data that drives learning. It's also the most school specific, the trickiest to define and the most susceptible to national change. We get this tool right first, and then move to summative assessment when it's established and working well.
8. **Enable data users to discover related information**. It's not easy to learn what data is out there.

#Simple Functional Specification
- Drag and drop ordering of school priorities. Priority affects who gets notified (e.g. priority group 1 might be he head/senior leader. If there are real concerns with an area of data, raise its priority!).
- Discovery of new reports/tests as you add them.
- Rules/tests are tagged/assigned to data groups, who have RACI owners.
- RACI grid determines who gets what when.
- Email notification.
- Overall view of how good the data is.
- Time view of individual tests, and the overall.
- Additional, advanced rules based on existing rule data sources

##Master data
- Groups (priority, contacts()).
- Contacts (email(s)).

##Core Data Objects
- Rule/Test. A rule is the basic building block. Each rule (within the MIS usually) creates an output file. No fails? No rows in the output. (Call it rule or test?).
- Log. Simple list of exceptions (errors) for a particular timestamp.

##Application Workflow (Assuming deployment correct).
- Scheduled rules run over a period of time. Rules create files in secure folder.
- Application triggers at defined cycle.
  1. Timestamp.
  2. Access secure folder.
  3. For each file in folder structure:
    1. Get file metadata (time, number of records, group from filename, owner RACI from filename). Save metadata to metadata log.
    2. Load data.
    3. (Get advanced/preprocessing rules and act on them).
    3. For each error found, log the full data of the error into the current log.
    4. Check the current log against the last log, and increment any recurrences in the current log.
    5. (Get postprocessing rules and act on them?).
    6. Delete the source file?
  4. Act on the current log, using the [RACI definitions](http://www.itsmprofessor.net/2010/10/why-use-raci-matrix.html) for the group of each report.
    1. For each report, get Responsible, Accountable, Consult, Inform of the group of that report. 
    2. If Responsible, notify of all errors.
    3. If Accountable, notify of serious and recurring errors.
    4. If Consult, do nothing. Maybe monthly/termly update? 
    5. If Inform, give overview only?
  5. Update visual dashboard. 
- Notify top level owners of outcome of cycle.
- Clearup.

