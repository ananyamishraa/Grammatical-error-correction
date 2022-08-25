# Grammatical-error-correction
# using python
import language_tool_python
tool_used = language_tool_python.LanguageTool('en-US')
text = """she are smart"""
check = tool_used.check(text)

Mistake = []
Corrections = []
start = []
end = []

for rules in check:
    if len(rules.replacements) > 0:
        start.append(rules.offset) #offset - to perform operations within the text file depending on the permissions given, like read, write
        end.append(rules.errorLength + rules.offset)
        Mistake.append(text[rules.offset: rules.errorLength + rules.offset])
        Corrections.append(rules.replacements[0])

Newtext = list(text)
for n in range(len(start)):
    for i in range(len(text)):
        Newtext[start[n]] = Corrections[n]
        if (i > start[n] and i < end[n]):
            Newtext[i] = ""

Newtext = "".join(Newtext) #to remove the spaces
print(Newtext)
