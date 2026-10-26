---
inbox_folder_id: cd30cf94-0967-489e-9c84-d720bb61852b
---
# Inbox Form

Choose an existing folder or click **Create inbox** and enter a character name.
The form remembers its destination and follows folder renames and moves.
Keep the automatically created **_Inbox Settings** note inside its inbox; it provides that connection.

New submissions include **Reply** and **Forward** buttons. A plain forward moves the submission.
A reply or a forward with a message starts a shared conversation in **Threads**, with an entry in every inbox it has visited.
Open any entry and click **Open thread** to read the full conversation.

This is local fictional correspondence; these buttons do not send email.
The form installs its shared controls in **_Papertrail** automatically. Keep that support folder.
Only submissions created with this version get the new controls. Existing notes are left untouched.


```js-engine

const { Notice, TFolder, TFile, Modal, normalizePath, stringifyYaml, parseYaml } = obsidian;


// Install shared controls automatically; no separate script setup is needed.
const runtimeSource = new TextDecoder().decode(Uint8Array.from(atob("Ly8gUGFwZXJ0cmFpbCBJbmJveCBBY3Rpb25zIHYxIOKAlCBsb2NhbCBmaWN0aW9uYWwgY29ycmVzcG9uZGVuY2UsIG5vIGVtYWlsIHRyYW5zcG9ydC4KY29uc3QgeyBURmlsZSwgVEZvbGRlciwgTW9kYWwsIE5vdGljZSwgcGFyc2VZYW1sLCBzdHJpbmdpZnlZYW1sIH0gPSBvYnNpZGlhbjsKY29uc3QgbWFya2VyTmFtZSA9ICdfSW5ib3ggU2V0dGluZ3MubWQnOwpjb25zdCBzZXBhcmF0b3IgPSAnXG48IS0tIHBhcGVydHJhaWwtYWN0aW9ucyAtLT5cbic7CmNvbnN0IHJ1bnRpbWVQYXRoID0gJ19QYXBlcnRyYWlsL0luYm94IEFjdGlvbnMuanMnOwpmdW5jdGlvbiB1bnBhY2sodGV4dCkgewogIGNvbnN0IG0gPSB0ZXh0Lm1hdGNoKC9eLS0tXHI/XG4oW1xzXFNdKj8pXHI/XG4tLS0oPzpccj9cbnwkKS8pOwogIHJldHVybiB7IGZtOiBtID8gKHBhcnNlWWFtbChtWzFdKSB8fCB7fSkgOiB7fSwgYm9keTogbSA/IHRleHQuc2xpY2UobVswXS5sZW5ndGgpIDogdGV4dCB9Owp9CmNvbnN0IHBhY2sgPSAoZm0sIGJvZHkpID0+IGAtLS1cbiR7c3RyaW5naWZ5WWFtbChmbSkudHJpbUVuZCgpfVxuLS0tXG5cbiR7Ym9keS50cmltU3RhcnQoKX1gOwpjb25zdCByZWFkID0gYXN5bmMgZmlsZSA9PiB1bnBhY2soYXdhaXQgYXBwLnZhdWx0LnJlYWQoZmlsZSkpOwpjb25zdCB1bmlxdWUgPSBsaXN0ID0+IFsuLi5uZXcgU2V0KGxpc3QuZmlsdGVyKEJvb2xlYW4pKV07CmNvbnN0IGxpbmUgPSB2YWx1ZSA9PiBTdHJpbmcodmFsdWUgfHwgJycpLnJlcGxhY2UoL1tcclxuXS9nLCAnICcpLnRyaW0oKTsKY29uc3Qgc2FmZSA9IHZhbHVlID0+IGxpbmUodmFsdWUpLnJlcGxhY2UoL1tcXC86Kj8iPD58I1xbXF1eXHUwMDAwLVx1MDAxZl0vZywgJyAnKS5yZXBsYWNlKC9ccysvZywgJyAnKS5zbGljZSgwLDEwMCkucmVwbGFjZSgvWy4gXSskL2csICcnKSB8fCAnQ29udmVyc2F0aW9uJzsKY29uc3QgbGlzdEZvbGRlcnMgPSAoKSA9PiBhcHAudmF1bHQuZ2V0QWxsTG9hZGVkRmlsZXMoKS5maWx0ZXIoZiA9PiBmIGluc3RhbmNlb2YgVEZvbGRlciAmJiAhZi5pc1Jvb3QoKSAmJiBmLnBhdGggIT09ICdUaHJlYWRzJyAmJiAhZi5wYXRoLnN0YXJ0c1dpdGgoJ1RocmVhZHMvJykgJiYgZi5wYXRoICE9PSAnX1BhcGVydHJhaWwnICYmICFmLnBhdGguc3RhcnRzV2l0aCgnX1BhcGVydHJhaWwvJykpLnNvcnQoKGEsYikgPT4gYS5wYXRoLmxvY2FsZUNvbXBhcmUoYi5wYXRoKSk7CmFzeW5jIGZ1bmN0aW9uIGVuc3VyZUZvbGRlcihwYXRoKSB7CiAgbGV0IGYgPSBhcHAudmF1bHQuZ2V0QWJzdHJhY3RGaWxlQnlQYXRoKHBhdGgpOwogIGlmICghZikgeyB0cnkgeyBmID0gYXdhaXQgYXBwLnZhdWx0LmNyZWF0ZUZvbGRlcihwYXRoKTsgfSBjYXRjaChlKSB7IGYgPSBhcHAudmF1bHQuZ2V0QWJzdHJhY3RGaWxlQnlQYXRoKHBhdGgpOyBpZiAoIWYpIHRocm93IGU7IH0gfQogIGlmICghKGYgaW5zdGFuY2VvZiBURm9sZGVyKSkgdGhyb3cgbmV3IEVycm9yKGBBIGZpbGUgYmxvY2tzIHRoZSBmb2xkZXIgJHtwYXRofS5gKTsKICByZXR1cm4gZjsKfQphc3luYyBmdW5jdGlvbiBpbmJveElkKGZvbGRlcikgewogIGlmICghKGZvbGRlciBpbnN0YW5jZW9mIFRGb2xkZXIpIHx8IGZvbGRlci5pc1Jvb3QoKSkgdGhyb3cgbmV3IEVycm9yKCdDaG9vc2UgYW4gaW5ib3ggZm9sZGVyLicpOwogIGNvbnN0IHBhdGggPSBgJHtmb2xkZXIucGF0aH0vJHttYXJrZXJOYW1lfWA7CiAgbGV0IG1hcmtlciA9IGFwcC52YXVsdC5nZXRBYnN0cmFjdEZpbGVCeVBhdGgocGF0aCk7CiAgaWYgKCFtYXJrZXIpIHsKICAgIGNvbnN0IGlkID0gY3J5cHRvLnJhbmRvbVVVSUQoKTsKICAgIHRyeSB7CiAgICAgIGF3YWl0IGFwcC52YXVsdC5jcmVhdGUocGF0aCwgcGFjayh7aW5ib3hfZm9sZGVyX2lkOmlkfSwgJyMgSW5ib3ggU2V0dGluZ3NcblxuS2VlcCB0aGlzIG5vdGUgaW5zaWRlIHRoZSBpbmJveCwgd2l0aCBpdHMgZmlsZW5hbWUgdW5jaGFuZ2VkLiBJdCBsZXRzIGZvcm1zIGFuZCBjb252ZXJzYXRpb25zIGZvbGxvdyBmb2xkZXIgcmVuYW1lcy5cbicpKTsKICAgICAgcmV0dXJuIGlkOwogICAgfSBjYXRjaChlKSB7IG1hcmtlciA9IGFwcC52YXVsdC5nZXRBYnN0cmFjdEZpbGVCeVBhdGgocGF0aCk7IGlmICghbWFya2VyKSB0aHJvdyBlOyB9CiAgfQogIGlmICghKG1hcmtlciBpbnN0YW5jZW9mIFRGaWxlKSkgdGhyb3cgbmV3IEVycm9yKCdJbmJveCBzZXR0aW5ncyBtdXN0IGJlIGEgbm90ZS4nKTsKICBjb25zdCBpZCA9IChhd2FpdCByZWFkKG1hcmtlcikpLmZtLmluYm94X2ZvbGRlcl9pZDsKICBpZiAodHlwZW9mIGlkICE9PSAnc3RyaW5nJyB8fCAhaWQpIHRocm93IG5ldyBFcnJvcihgQW4gdW5yZWxhdGVkICR7bWFya2VyTmFtZX0gbm90ZSBhbHJlYWR5IGV4aXN0cyBpbiB0aGlzIGZvbGRlci5gKTsKICByZXR1cm4gaWQ7Cn0KYXN5bmMgZnVuY3Rpb24gaW5ib3hlcygpIHsKICBjb25zdCBtYXAgPSBuZXcgTWFwKCk7CiAgZm9yIChjb25zdCBmaWxlIG9mIGFwcC52YXVsdC5nZXRNYXJrZG93bkZpbGVzKCkuZmlsdGVyKGYgPT4gZi5uYW1lID09PSBtYXJrZXJOYW1lKSkgewogICAgY29uc3QgaWQgPSAoYXdhaXQgcmVhZChmaWxlKSkuZm0uaW5ib3hfZm9sZGVyX2lkOwogICAgaWYgKCFpZCkgY29udGludWU7CiAgICBpZiAobWFwLmhhcyhpZCkpIHRocm93IG5ldyBFcnJvcignVHdvIGluYm94ZXMgc2hhcmUgYSBjb3BpZWQgc2V0dGluZ3Mgbm90ZS4gUmVtb3ZlIHRoZSBzZXR0aW5ncyBub3RlIGZyb20gdGhlIGNvcGllZCBmb2xkZXIgYW5kIHNlbGVjdCB0aGF0IGZvbGRlciBhZ2Fpbi4nKTsKICAgIG1hcC5zZXQoaWQsIGZpbGUucGFyZW50KTsKICB9CiAgcmV0dXJuIG1hcDsKfQphc3luYyBmdW5jdGlvbiBjYW5vbmljYWwoaWQpIHsKICBjb25zdCBtYXRjaGVzPVtdOwogIGZvciAoY29uc3QgZiBvZiBhcHAudmF1bHQuZ2V0TWFya2Rvd25GaWxlcygpKSB7CiAgICBjb25zdCBmbT0oYXdhaXQgcmVhZChmKSkuZm07CiAgICBpZiAoZm0ucGFwZXJ0cmFpbF9pZCA9PT0gaWQgJiYgWydzdWJtaXNzaW9uJywndGhyZWFkJ10uaW5jbHVkZXMoZm0ucGFwZXJ0cmFpbF9raW5kKSkgbWF0Y2hlcy5wdXNoKGYpOwogIH0KICBpZiAobWF0Y2hlcy5sZW5ndGggIT09IDEpIHRocm93IG5ldyBFcnJvcihtYXRjaGVzLmxlbmd0aCA/ICdEdXBsaWNhdGUgY29udmVyc2F0aW9uIG5vdGVzIGZvdW5kLiBLZWVwIG9uZSBvcmlnaW5hbCBjb252ZXJzYXRpb24uJyA6ICdUaGUgY29udmVyc2F0aW9uIG5vdGUgY291bGQgbm90IGJlIGZvdW5kLicpOwogIHJldHVybiBtYXRjaGVzWzBdOwp9CmFzeW5jIGZ1bmN0aW9uIGZyZWVQYXRoKGZvbGRlciwgZmlsZW5hbWUsIHNlbGYpIHsKICBjb25zdCBzdGVtPWZpbGVuYW1lLnJlcGxhY2UoL1wubWQkLywgJycpOwogIGZvcihsZXQgbj0wOztuKyspIHsKICAgIGNvbnN0IHBhdGg9YCR7Zm9sZGVyfS8ke3N0ZW19JHtuID8gYCAoJHtufSlgIDogJyd9Lm1kYDsKICAgIGNvbnN0IGZvdW5kPWFwcC52YXVsdC5nZXRBYnN0cmFjdEZpbGVCeVBhdGgocGF0aCk7CiAgICBpZighZm91bmQgfHwgZm91bmQ9PT1zZWxmKSByZXR1cm4gcGF0aDsKICB9Cn0KY29uc3QgYm9vdHN0cmFwID0gJ2BgYGpzLWVuZ2luZVxuY29uc3QgcnVudGltZSA9IGFwcC52YXVsdC5nZXRBYnN0cmFjdEZpbGVCeVBhdGgoIl9QYXBlcnRyYWlsL0luYm94IEFjdGlvbnMuanMiKTtcbmlmICghcnVudGltZSkgeyBjb250YWluZXIuY3JlYXRlRWwoInAiLCB7dGV4dDogIk9wZW4gSW5ib3ggRm9ybSB0byBpbnN0YWxsIHRoZSBjb252ZXJzYXRpb24gY29udHJvbHMuIn0pOyB9IGVsc2Uge1xuY29uc3QgcnVuID0gT2JqZWN0LmdldFByb3RvdHlwZU9mKGFzeW5jIGZ1bmN0aW9uKCl7fSkuY29uc3RydWN0b3I7XG5hd2FpdCBuZXcgcnVuKCJhcHAiLCAib2JzaWRpYW4iLCAiY29udGV4dCIsICJjb250YWluZXIiLCAiY29tcG9uZW50IiwgYXdhaXQgYXBwLnZhdWx0LnJlYWQocnVudGltZSkpKGFwcCwgb2JzaWRpYW4sIGNvbnRleHQsIGNvbnRhaW5lciwgY29tcG9uZW50KTtcbn1cbmBgYCc7CmFzeW5jIGZ1bmN0aW9uIGVudHJpZXMoZmlsZSkgewogIGNvbnN0IHtmbX09YXdhaXQgcmVhZChmaWxlKTsKICBjb25zdCBmb2xkZXJzPWF3YWl0IGluYm94ZXMoKTsKICBjb25zdCBtaXNzaW5nPVtdOwogIGZvcihjb25zdCBpZCBvZiB1bmlxdWUoZm0udmlzaXRlZF9pbmJveGVzIHx8IFtdKSkgewogICAgY29uc3QgZm9sZGVyPWZvbGRlcnMuZ2V0KGlkKTsKICAgIGlmKCFmb2xkZXIpIHsgbWlzc2luZy5wdXNoKGlkKTtjb250aW51ZTsgfQogICAgbGV0IGV4aXN0cz1mYWxzZTsKICAgIGZvcihjb25zdCBmIG9mIGFwcC52YXVsdC5nZXRNYXJrZG93bkZpbGVzKCkuZmlsdGVyKGY9PmYucGFyZW50PT09Zm9sZGVyKSkgewogICAgICBjb25zdCBwcm9wcz0oYXdhaXQgcmVhZChmKSkuZm07CiAgICAgIGlmKHByb3BzLnBhcGVydHJhaWxfa2luZD09PSdpbmJveC1saW5rJyAmJiBwcm9wcy5wYXBlcnRyYWlsX2lkPT09Zm0ucGFwZXJ0cmFpbF9pZCkge2V4aXN0cz10cnVlO2JyZWFrO30KICAgIH0KICAgIGlmKGV4aXN0cykgY29udGludWU7CiAgICBjb25zdCBwYXRoPWF3YWl0IGZyZWVQYXRoKGZvbGRlci5wYXRoLGAke3NhZmUoZm0uc3ViamVjdCl9IC0gdGhyZWFkICR7Zm0ucGFwZXJ0cmFpbF9pZC5zbGljZSgwLDgpfS5tZGApOwogICAgLy8gSUQtYmFzZWQgT3BlbiB0aHJlYWQgY29udHJvbCBzdXJ2aXZlcyByZW5hbWVzIHdpdGhvdXQgcmVseWluZyBvbiBPYnNpZGlhbidzIGxpbmsgc2V0dGluZ3MuCiAgICBhd2FpdCBhcHAudmF1bHQuY3JlYXRlKHBhdGgscGFjayh7cGFwZXJ0cmFpbF9raW5kOidpbmJveC1saW5rJyxwYXBlcnRyYWlsX2lkOmZtLnBhcGVydHJhaWxfaWQsaW5ib3hfZm9sZGVyX2lkOmlkLHN1YmplY3Q6Zm0uc3ViamVjdH0sYCMgJHtzYWZlKGZtLnN1YmplY3QpfVxuXG5UaGlzIGluYm94IGhhcyBhY2Nlc3MgdG8gdGhlIHNoYXJlZCBjb252ZXJzYXRpb24uXG5cbiR7Ym9vdHN0cmFwfVxuYCkpOwogIH0KICBpZihtaXNzaW5nLmxlbmd0aCkgbmV3IE5vdGljZShgJHttaXNzaW5nLmxlbmd0aH0gZWFybGllciBpbmJveCBmb2xkZXIocykgY291bGQgbm90IGJlIGZvdW5kLiBUaGUgY29udmVyc2F0aW9uIGlzIHNhdmVkOyByZXN0b3JlIHRoZWlyIHNldHRpbmdzIG5vdGVzLCB0aGVuIHVzZSBSZXBhaXIgaW5ib3ggbGlua3MuYCk7Cn0KYXN5bmMgZnVuY3Rpb24gcHJvbW90ZShmaWxlKSB7CiAgY29uc3Qge2ZtfT1hd2FpdCByZWFkKGZpbGUpOwogIGlmKGZtLnBhcGVydHJhaWxfa2luZCE9PSd0aHJlYWQnKSByZXR1cm47CiAgLy8gT25seSBhdXRvbWF0aWNhbGx5IG1vdmUgYSBjb252ZXJzYXRpb24gb24gaXRzIGZpcnN0IHByb21vdGlvbi4KICBpZighZm0udGhyZWFkX2hvbWVfc2V0KSB7CiAgICBhd2FpdCBlbnN1cmVGb2xkZXIoJ1RocmVhZHMnKTsKICAgIGNvbnN0IHBhdGg9YXdhaXQgZnJlZVBhdGgoJ1RocmVhZHMnLGZpbGUubmFtZSxmaWxlKTsKICAgIGlmKGZpbGUucGF0aCE9PXBhdGgpIGF3YWl0IGFwcC5maWxlTWFuYWdlci5yZW5hbWVGaWxlKGZpbGUscGF0aCk7CiAgICBhd2FpdCBhcHAuZmlsZU1hbmFnZXIucHJvY2Vzc0Zyb250TWF0dGVyKGZpbGUscD0+e3AudGhyZWFkX2hvbWVfc2V0PXRydWU7fSk7CiAgfQogIGF3YWl0IGVudHJpZXMoZmlsZSk7Cn0KYXN5bmMgZnVuY3Rpb24gYXBwbHlBY3Rpb24oaWQsIGFjdGlvbikgewogIGNvbnN0IGxvY2tLZXk9U3ltYm9sLmZvcigncGFwZXJ0cmFpbC5pbmJveC5sb2NrcycpOwogIGNvbnN0IGxvY2tzPWFwcFtsb2NrS2V5XSB8fCAoYXBwW2xvY2tLZXldPW5ldyBTZXQoKSk7CiAgaWYobG9ja3MuaGFzKGlkKSkgdGhyb3cgbmV3IEVycm9yKCdUaGlzIGNvbnZlcnNhdGlvbiBpcyBzYXZpbmcgaW4gYW5vdGhlciB3aW5kb3cuIFRyeSBhZ2FpbiBzaG9ydGx5LicpOwogIGxvY2tzLmFkZChpZCk7CiAgdHJ5IHsKICAgIGNvbnN0IGZpbGU9YXdhaXQgY2Fub25pY2FsKGlkKTsKICAgIGxldCB7Zm19PWF3YWl0IHJlYWQoZmlsZSk7CiAgICAvLyBBIHJldHJ5IHJlcGFpcnMgYW55IGludGVycnVwdGVkIG1vdmUvbGluayBjcmVhdGlvbiB3aXRob3V0IGFwcGVuZGluZyB0d2ljZS4KICAgIGlmKChmbS5jb21wbGV0ZWRfYWN0aW9ucyB8fCBbXSkuaW5jbHVkZXMoYWN0aW9uLmlkKSkgewogICAgICBhd2FpdCBwcm9tb3RlKGZpbGUpO3JldHVybiBmaWxlOwogICAgfQogICAgY29uc3QgZm9sZGVycz1hd2FpdCBpbmJveGVzKCk7CiAgICBsZXQgZnJvbT1mb2xkZXJzLmdldChhY3Rpb24uZnJvbUlkKTsKICAgIGlmKCFmcm9tKSB0aHJvdyBuZXcgRXJyb3IoJ1RoZSBzZW5kaW5nIGluYm94IGlzIG1pc3NpbmcuIENsb3NlIHRoaXMgZGlhbG9nIGFuZCBzZWxlY3QgYW4gaW5ib3ggYWdhaW4uJyk7CiAgICBsZXQgZGVzdGluYXRpb247CiAgICBpZihhY3Rpb24ubW9kZT09PSdmb3J3YXJkJykgewogICAgICBkZXN0aW5hdGlvbj1hcHAudmF1bHQuZ2V0QWJzdHJhY3RGaWxlQnlQYXRoKGFjdGlvbi50b1BhdGgpOwogICAgICBpZighKGRlc3RpbmF0aW9uIGluc3RhbmNlb2YgVEZvbGRlcikpIHRocm93IG5ldyBFcnJvcignQ2hvb3NlIGFuIGV4aXN0aW5nIGRlc3RpbmF0aW9uIGluYm94LicpOwogICAgICBhY3Rpb24udG9JZD1hd2FpdCBpbmJveElkKGRlc3RpbmF0aW9uKTsKICAgICAgaWYoYWN0aW9uLnRvSWQ9PT1hY3Rpb24uZnJvbUlkKSB0aHJvdyBuZXcgRXJyb3IoJ0Nob29zZSBhIGRpZmZlcmVudCBkZXN0aW5hdGlvbiBpbmJveC4nKTsKICAgIH0KICAgIGNvbnN0IGJhcmU9Zm0ucGFwZXJ0cmFpbF9raW5kPT09J3N1Ym1pc3Npb24nICYmIGFjdGlvbi5tb2RlPT09J2ZvcndhcmQnICYmICFhY3Rpb24ubWVzc2FnZS50cmltKCk7CiAgICBpZihiYXJlKSB7CiAgICAgIC8vIFJlY29yZCBhIHBsYW5uZWQgbW92ZSBmaXJzdCBzbyBhbiBpbnRlcnJ1cHRlZCBtb3ZlIGlzIHNhZmVseSByZXRyeWFibGUuCiAgICAgIGF3YWl0IGFwcC5maWxlTWFuYWdlci5wcm9jZXNzRnJvbnRNYXR0ZXIoZmlsZSxwPT57CiAgICAgICAgcC52aXNpdGVkX2luYm94ZXM9dW5pcXVlKFsuLi4ocC52aXNpdGVkX2luYm94ZXN8fFtdKSxhY3Rpb24uZnJvbUlkLGFjdGlvbi50b0lkXSk7CiAgICAgIH0pOwogICAgICBjb25zdCB0YXJnZXQ9YXdhaXQgZnJlZVBhdGgoZGVzdGluYXRpb24ucGF0aCxmaWxlLm5hbWUsZmlsZSk7CiAgICAgIGlmKGZpbGUucGF0aCE9PXRhcmdldCkgYXdhaXQgYXBwLmZpbGVNYW5hZ2VyLnJlbmFtZUZpbGUoZmlsZSx0YXJnZXQpOwogICAgICBhd2FpdCBhcHAuZmlsZU1hbmFnZXIucHJvY2Vzc0Zyb250TWF0dGVyKGZpbGUscD0+ewogICAgICAgIHAuY3VycmVudF9pbmJveF9pZD1hY3Rpb24udG9JZDsKICAgICAgICBwLmNvbXBsZXRlZF9hY3Rpb25zPXVuaXF1ZShbLi4uKHAuY29tcGxldGVkX2FjdGlvbnN8fFtdKSxhY3Rpb24uaWRdKTsKICAgICAgfSk7CiAgICAgIHJldHVybiBmaWxlOwogICAgfQogICAgY29uc3QgdG89YWN0aW9uLm1vZGU9PT0nZm9yd2FyZCcgPyBkZXN0aW5hdGlvbi5wYXRoIDogbGluZShhY3Rpb24udG8pOwogICAgY29uc3QgZnJvbU5hbWU9bGluZShhY3Rpb24uc2VuZGVyKSB8fCBmcm9tLnBhdGg7CiAgICBjb25zdCBoZWFkaW5nPWFjdGlvbi5tb2RlPT09J3JlcGx5JyA/ICdSZXBseScgOiBhY3Rpb24ubWVzc2FnZS50cmltKCkgPyAnRm9yd2FyZCB3aXRoIG1lc3NhZ2UnIDogJ0ZvcndhcmQnOwogICAgY29uc3QgdGltZXN0YW1wPW5ldyBEYXRlKCkudG9JU09TdHJpbmcoKTsKICAgIGNvbnN0IGFkZGl0aW9uPWBcblxuLS0tXG5cbiMjICR7aGVhZGluZ31cblxuKipGcm9tOioqICR7ZnJvbU5hbWV9ICBcbioqVG86KiogJHt0b30gIFxuKipEYXRlOioqICR7dGltZXN0YW1wfVxuXG4ke2FjdGlvbi5tZXNzYWdlLnRyaW0oKSB8fCAnX0ZvcndhcmRlZCB3aXRob3V0IGFuIGFkZGl0aW9uYWwgbWVzc2FnZS5fJ31cbmA7CiAgICBhd2FpdCBhcHAudmF1bHQucHJvY2VzcyhmaWxlLHRleHQ9PnsKICAgICAgY29uc3QgZG9jPXVucGFjayh0ZXh0KTsKICAgICAgaWYoKGRvYy5mbS5jb21wbGV0ZWRfYWN0aW9uc3x8W10pLmluY2x1ZGVzKGFjdGlvbi5pZCkpIHJldHVybiB0ZXh0OwogICAgICBjb25zdCBzcGxpdD1kb2MuYm9keS5pbmRleE9mKHNlcGFyYXRvcik7CiAgICAgIGlmKHNwbGl0PDApIHRocm93IG5ldyBFcnJvcignVGhlIGNvbnZlcnNhdGlvbiBjb250cm9scyBtYXJrZXIgaXMgbWlzc2luZy4gUmVzdG9yZSBpdCBiZWZvcmUgcmVwbHlpbmcuJyk7CiAgICAgIGRvYy5mbS5wYXBlcnRyYWlsX2tpbmQ9J3RocmVhZCc7CiAgICAgIGRvYy5mbS52aXNpdGVkX2luYm94ZXM9dW5pcXVlKFsuLi4oZG9jLmZtLnZpc2l0ZWRfaW5ib3hlc3x8W10pLGFjdGlvbi5mcm9tSWQsYWN0aW9uLnRvSWRdKTsKICAgICAgZG9jLmZtLmNvbXBsZXRlZF9hY3Rpb25zPXVuaXF1ZShbLi4uKGRvYy5mbS5jb21wbGV0ZWRfYWN0aW9uc3x8W10pLGFjdGlvbi5pZF0pOwogICAgICBkb2MuZm0ubGFzdF91cGRhdGVkPXRpbWVzdGFtcDsKICAgICAgcmV0dXJuIHBhY2soZG9jLmZtLGRvYy5ib2R5LnNsaWNlKDAsc3BsaXQpLnRyaW1FbmQoKSthZGRpdGlvbitkb2MuYm9keS5zbGljZShzcGxpdCkpOwogICAgfSk7CiAgICBhd2FpdCBwcm9tb3RlKGZpbGUpOwogICAgcmV0dXJuIGZpbGU7CiAgfSBmaW5hbGx5IHtsb2Nrcy5kZWxldGUoaWQpO30KfQovLyBJbnRlcm5hbCB0ZXN0IGhvb2s7IHVudXNlZCBieSB0aGUgZm9ybSBvciBnZW5lcmF0ZWQgbm90ZXMuCmlmKHR5cGVvZiB0ZXN0aW5nIT09J3VuZGVmaW5lZCcpIHJldHVybiB7YXBwbHlBY3Rpb24scmVhZCxpbmJveElkLGluYm94ZXMsY2Fub25pY2FsLGVudHJpZXMsYm9vdHN0cmFwLHNlcGFyYXRvcn07CmNvbnN0IGluaXRpYWw9YXdhaXQgcmVhZChjb250ZXh0LmZpbGUpOwpjb25zdCBjb252ZXJzYXRpb25JZD1pbml0aWFsLmZtLnBhcGVydHJhaWxfaWQ7CmlmKCFjb252ZXJzYXRpb25JZCkge2NvbnRhaW5lci5jcmVhdGVFbCgncCcse3RleHQ6J1RoaXMgbm90ZSBkb2VzIG5vdCBoYXZlIGEgUGFwZXJ0cmFpbCBjb252ZXJzYXRpb24gSUQuJ30pO3JldHVybjt9CmNvbnN0IGNhbm9uaWNhbEZpbGU9YXdhaXQgY2Fub25pY2FsKGNvbnZlcnNhdGlvbklkKTsKY29uc3QgY3VycmVudD1hd2FpdCByZWFkKGNhbm9uaWNhbEZpbGUpOwpjb25zdCB0b29sYmFyPWNvbnRhaW5lci5jcmVhdGVEaXYoKTsKT2JqZWN0LmFzc2lnbih0b29sYmFyLnN0eWxlLHtkaXNwbGF5OidmbGV4JyxmbGV4V3JhcDond3JhcCcsZ2FwOicxMHB4JyxwYWRkaW5nVG9wOicxNnB4Jyxib3JkZXJUb3A6JzFweCBzb2xpZCB2YXIoLS1iYWNrZ3JvdW5kLW1vZGlmaWVyLWJvcmRlciknfSk7CmNvbnN0IHN0YXR1cz1jb250YWluZXIuY3JlYXRlRWwoJ3AnLHthdHRyOntyb2xlOidzdGF0dXMnLCdhcmlhLWxpdmUnOidwb2xpdGUnfX0pOwphc3luYyBmdW5jdGlvbiBvcGVuVGhyZWFkKCkge2F3YWl0IGFwcC53b3Jrc3BhY2UuZ2V0TGVhZihmYWxzZSkub3BlbkZpbGUoYXdhaXQgY2Fub25pY2FsKGNvbnZlcnNhdGlvbklkKSk7fQppZihpbml0aWFsLmZtLnBhcGVydHJhaWxfa2luZD09PSdpbmJveC1saW5rJykgewogIGNvbnN0IG9wZW49dG9vbGJhci5jcmVhdGVFbCgnYnV0dG9uJyx7dGV4dDonT3BlbiB0aHJlYWQnLGNsczonbW9kLWN0YSd9KTsKICBvcGVuLmFkZEV2ZW50TGlzdGVuZXIoJ2NsaWNrJywoKT0+b3BlblRocmVhZCgpLmNhdGNoKGU9PntzdGF0dXMudGV4dENvbnRlbnQ9ZS5tZXNzYWdlO30pKTsKfQpjbGFzcyBBY3Rpb25Nb2RhbCBleHRlbmRzIE1vZGFsIHsKICBjb25zdHJ1Y3Rvcihtb2RlKXtzdXBlcihhcHApO3RoaXMubW9kZT1tb2RlO3RoaXMub3BlcmF0aW9uSWQ9Y3J5cHRvLnJhbmRvbVVVSUQoKTt9CiAgb25PcGVuKCl7dGhpcy5idWlsZCgpLmNhdGNoKGU9Pnt0aGlzLmNvbnRlbnRFbC5jcmVhdGVFbCgncCcse3RleHQ6ZS5tZXNzYWdlfSk7fSk7fQogIGFzeW5jIGJ1aWxkKCl7CiAgICBjb25zdCBtb2RlPXRoaXMubW9kZTsKICAgIGNvbnN0IGZpbGU9YXdhaXQgY2Fub25pY2FsKGNvbnZlcnNhdGlvbklkKSwge2ZtfT1hd2FpdCByZWFkKGZpbGUpOwogICAgY29uc3QgZm9sZGVycz1hd2FpdCBpbmJveGVzKCk7CiAgICB0aGlzLmNvbnRlbnRFbC5jcmVhdGVFbCgnaDInLHt0ZXh0Om1vZGU9PT0ncmVwbHknPydSZXBseSc6J0ZvcndhcmQnfSk7CiAgICB0aGlzLmNvbnRlbnRFbC5jcmVhdGVFbCgncCcse3RleHQ6Zm0uc3ViamVjdH0pOwogICAgY29uc3QgcGFuZWw9dGhpcy5jb250ZW50RWwuY3JlYXRlRWwoJ2Zvcm0nKTsKICAgIE9iamVjdC5hc3NpZ24ocGFuZWwuc3R5bGUse2Rpc3BsYXk6J2dyaWQnLGdhcDonMTRweCd9KTsKICAgIGZ1bmN0aW9uIGZpZWxkKGxhYmVsLHRhZz0naW5wdXQnKXsKICAgICAgY29uc3Qgd3JhcHBlcj1wYW5lbC5jcmVhdGVFbCgnbGFiZWwnLHt0ZXh0OmxhYmVsfSk7CiAgICAgIGNvbnN0IGlucHV0PXdyYXBwZXIuY3JlYXRlRWwodGFnKTtpbnB1dC5zdHlsZS53aWR0aD0nMTAwJSc7aW5wdXQuc3R5bGUubWFyZ2luVG9wPSc2cHgnO3JldHVybiBpbnB1dDsKICAgIH0KICAgIGNvbnN0IGZyb209ZmllbGQobW9kZT09PSdyZXBseSc/J1JlcGx5IGZyb20gaW5ib3gnOidGb3J3YXJkIGZyb20gaW5ib3gnLCdzZWxlY3QnKTtmcm9tLnJlcXVpcmVkPXRydWU7CiAgICBmb3IoY29uc3QgaWQgb2YgdW5pcXVlKGZtLnZpc2l0ZWRfaW5ib3hlc3x8W10pKSBpZihmb2xkZXJzLmhhcyhpZCkpIGZyb20uY3JlYXRlRWwoJ29wdGlvbicse3RleHQ6Zm9sZGVycy5nZXQoaWQpLnBhdGgsdmFsdWU6aWR9KTsKICAgIGZyb20udmFsdWU9aW5pdGlhbC5mbS5wYXBlcnRyYWlsX2tpbmQ9PT0naW5ib3gtbGluaycgPyBpbml0aWFsLmZtLmluYm94X2ZvbGRlcl9pZCA6IGZtLmN1cnJlbnRfaW5ib3hfaWQgfHwgKGZtLnZpc2l0ZWRfaW5ib3hlc3x8W10pLmF0KC0xKSB8fCAnJzsKICAgIGlmKCFmcm9tLnZhbHVlICYmIGZyb20ub3B0aW9ucy5sZW5ndGgpIGZyb20uc2VsZWN0ZWRJbmRleD0wOwogICAgY29uc3Qgc2VuZGVyPWZpZWxkKCdGcm9tIChjaGFyYWN0ZXIgbmFtZSBvciBlbWFpbCknKTsKICAgIGNvbnN0IHVwZGF0ZVNlbmRlcj0oKT0+e3NlbmRlci52YWx1ZT1mb2xkZXJzLmdldChmcm9tLnZhbHVlKT8ucGF0aC5zcGxpdCgnLycpLnBvcCgpLnJlcGxhY2UoLyg/OuKAmXN8J3MpIEluYm94JC9pLCcnKSB8fCAnJzt9OwogICAgLy8gRm9sZGVyIHBhdGhzIGFyZSB0aGUgZGVmYXVsdCBpZGVudGl0eTsgdGhlIGF1dGhvciBjYW4gZW50ZXIgYW55IGNoYXJhY3RlciBuYW1lL2VtYWlsLgogICAgc2VuZGVyLnZhbHVlPWZvbGRlcnMuZ2V0KGZyb20udmFsdWUpPy5wYXRoLnNwbGl0KCcvJykucG9wKCkucmVwbGFjZSgvKD864oCZc3wncykgSW5ib3gkL2ksJycpIHx8ICcnOwogICAgZnJvbS5hZGRFdmVudExpc3RlbmVyKCdjaGFuZ2UnLHVwZGF0ZVNlbmRlcik7c2VuZGVyLnJlcXVpcmVkPXRydWU7CiAgICBjb25zdCB0bz1maWVsZChtb2RlPT09J3JlcGx5Jz8nVG8gKG5hbWUgb3IgZW1haWwpJzonRGVzdGluYXRpb24gaW5ib3gnLG1vZGU9PT0ncmVwbHknPydpbnB1dCc6J3NlbGVjdCcpO3RvLnJlcXVpcmVkPXRydWU7CiAgICBpZihtb2RlPT09J3JlcGx5JykgdG8udmFsdWU9Zm0uZW1haWx8fCcnOwogICAgZWxzZSB7dG8uY3JlYXRlRWwoJ29wdGlvbicse3RleHQ6J0Nob29zZSBhbiBpbmJveOKApicsdmFsdWU6Jyd9KTtmb3IoY29uc3QgZm9sZGVyIG9mIGxpc3RGb2xkZXJzKCkpIHRvLmNyZWF0ZUVsKCdvcHRpb24nLHt0ZXh0OmZvbGRlci5wYXRoLHZhbHVlOmZvbGRlci5wYXRofSk7fQogICAgY29uc3QgbWVzc2FnZT1maWVsZChtb2RlPT09J3JlcGx5Jz8nTWVzc2FnZSc6J01lc3NhZ2UgKG9wdGlvbmFsKScsJ3RleHRhcmVhJyk7bWVzc2FnZS5yb3dzPTg7bWVzc2FnZS5zdHlsZS5yZXNpemU9J3ZlcnRpY2FsJzttZXNzYWdlLnJlcXVpcmVkPW1vZGU9PT0ncmVwbHknOwogICAgaWYobW9kZT09PSdmb3J3YXJkJykgcGFuZWwuY3JlYXRlRWwoJ3NtYWxsJyx7dGV4dDonTGVhdmUgYmxhbmsgdG8gbW92ZSBhIHN0YW5kYWxvbmUgc3VibWlzc2lvbi4gQWRkaW5nIGEgbWVzc2FnZSBzdGFydHMgYSB0aHJlYWQuIEV4aXN0aW5nIHRocmVhZHMgcmVtYWluIHNoYXJlZC4nfSk7CiAgICBjb25zdCBlcnJvcj1wYW5lbC5jcmVhdGVFbCgncCcse2F0dHI6e3JvbGU6J2FsZXJ0J319KTsKICAgIGNvbnN0IHNlbmQ9cGFuZWwuY3JlYXRlRWwoJ2J1dHRvbicse3RleHQ6bW9kZT09PSdyZXBseSc/J1NhdmUgcmVwbHknOidGb3J3YXJkJyx0eXBlOidzdWJtaXQnLGNsczonbW9kLWN0YSd9KTsKICAgIGNvbnN0IGNhbmNlbD1wYW5lbC5jcmVhdGVFbCgnYnV0dG9uJyx7dGV4dDonQ2FuY2VsJyx0eXBlOididXR0b24nfSk7Y2FuY2VsLmFkZEV2ZW50TGlzdGVuZXIoJ2NsaWNrJywoKT0+dGhpcy5jbG9zZSgpKTsKICAgIGxldCBzYXZpbmc9ZmFsc2U7CiAgICBwYW5lbC5hZGRFdmVudExpc3RlbmVyKCdzdWJtaXQnLGFzeW5jIGV2ZW50PT57CiAgICAgIGV2ZW50LnByZXZlbnREZWZhdWx0KCk7aWYoc2F2aW5nfHwhcGFuZWwucmVwb3J0VmFsaWRpdHkoKSlyZXR1cm47CiAgICAgIGlmKG1vZGU9PT0ncmVwbHknJiYhbWVzc2FnZS52YWx1ZS50cmltKCkpe2Vycm9yLnRleHRDb250ZW50PSdXcml0ZSBhIG1lc3NhZ2UgYmVmb3JlIHJlcGx5aW5nLic7cmV0dXJuO30KICAgICAgc2F2aW5nPXRydWU7c2VuZC5kaXNhYmxlZD10cnVlO2NhbmNlbC5kaXNhYmxlZD10cnVlOwogICAgICB0cnkgewogICAgICAgIGNvbnN0IHVwZGF0ZWQ9YXdhaXQgYXBwbHlBY3Rpb24oY29udmVyc2F0aW9uSWQse2lkOnRoaXMub3BlcmF0aW9uSWQsbW9kZSxmcm9tSWQ6ZnJvbS52YWx1ZSxzZW5kZXI6c2VuZGVyLnZhbHVlLHRvOnRvLnZhbHVlLHRvUGF0aDp0by52YWx1ZSxtZXNzYWdlOm1lc3NhZ2UudmFsdWV9KTsKICAgICAgICB0aGlzLmNsb3NlKCk7bmV3IE5vdGljZShtb2RlPT09J3JlcGx5Jz8nUmVwbHkgc2F2ZWQuJzonRm9yd2FyZGVkLicpOwogICAgICAgIGF3YWl0IGFwcC53b3Jrc3BhY2UuZ2V0TGVhZihmYWxzZSkub3BlbkZpbGUodXBkYXRlZCk7CiAgICAgIH0gY2F0Y2goZSl7ZXJyb3IudGV4dENvbnRlbnQ9YCR7ZS5tZXNzYWdlfSBZb3VyIG1lc3NhZ2UgaXMga2VwdCBoZXJlLiBSZXRyeSB0byBmaW5pc2ggc2FmZWx5LmA7c2VuZC50ZXh0Q29udGVudD0nUmV0cnknO30KICAgICAgZmluYWxseSB7c2F2aW5nPWZhbHNlO3NlbmQuZGlzYWJsZWQ9ZmFsc2U7Y2FuY2VsLmRpc2FibGVkPWZhbHNlO30KICAgIH0pOwogICAgbWVzc2FnZS5mb2N1cygpOwogIH0KICBvbkNsb3NlKCl7dGhpcy5jb250ZW50RWwuZW1wdHkoKTt9Cn0KZm9yKGNvbnN0IG1vZGUgb2YgWydyZXBseScsJ2ZvcndhcmQnXSl7CiAgY29uc3QgYnV0dG9uPXRvb2xiYXIuY3JlYXRlRWwoJ2J1dHRvbicse3RleHQ6bW9kZT09PSdyZXBseSc/J1JlcGx5JzonRm9yd2FyZCd9KTsKICBidXR0b24uYWRkRXZlbnRMaXN0ZW5lcignY2xpY2snLCgpPT5uZXcgQWN0aW9uTW9kYWwobW9kZSkub3BlbigpKTsKfQppZihjdXJyZW50LmZtLnBhcGVydHJhaWxfa2luZD09PSd0aHJlYWQnKSB7CiAgY29uc3QgcmVwYWlyPXRvb2xiYXIuY3JlYXRlRWwoJ2J1dHRvbicse3RleHQ6J1JlcGFpciBpbmJveCBsaW5rcyd9KTsKICByZXBhaXIuYWRkRXZlbnRMaXN0ZW5lcignY2xpY2snLGFzeW5jKCk9PntyZXBhaXIuZGlzYWJsZWQ9dHJ1ZTt0cnl7YXdhaXQgcHJvbW90ZShhd2FpdCBjYW5vbmljYWwoY29udmVyc2F0aW9uSWQpKTtzdGF0dXMudGV4dENvbnRlbnQ9J0luYm94IGxpbmtzIGNoZWNrZWQuJzt9Y2F0Y2goZSl7c3RhdHVzLnRleHRDb250ZW50PWUubWVzc2FnZTt9ZmluYWxseXtyZXBhaXIuZGlzYWJsZWQ9ZmFsc2U7fX0pOwp9Cg=="), c => c.charCodeAt(0)));
const controls = "\u0060\u0060\u0060js-engine\nconst runtime = app.vault.getAbstractFileByPath(\"_Papertrail/Inbox Actions.js\");\nif (!runtime) { container.createEl(\"p\", {text: \"Open Inbox Form to install the conversation controls.\"}); } else {\nconst run = Object.getPrototypeOf(async function(){}).constructor;\nawait new run(\"app\", \"obsidian\", \"context\", \"container\", \"component\", await app.vault.read(runtime))(app, obsidian, context, container, component);\n}\n\u0060\u0060\u0060";
async function installRuntime() {
  const home = "_Papertrail";
  const path = `${home}/Inbox Actions.js`;
  let folder = app.vault.getAbstractFileByPath(home);
  if (!folder) folder = await app.vault.createFolder(home);
  if (!(folder instanceof TFolder)) throw new Error("A note blocks the _Papertrail support folder.");
  const existing = app.vault.getAbstractFileByPath(path);
  if (!existing) await app.vault.create(path, runtimeSource);
  else {
    if (!(existing instanceof TFile)) throw new Error("Inbox Actions.js must be a file.");
    const text = await app.vault.read(existing);
    if (text !== runtimeSource) {
      if (!text.startsWith("// Papertrail Inbox Actions")) throw new Error("An unrelated Inbox Actions.js file already exists.");
      await app.vault.modify(existing, runtimeSource);
    }
  }
}
await installRuntime();

const form = container.createEl("form");
Object.assign(form.style, {
  display: "grid", gap: "16px", maxWidth: "620px",
  padding: "20px", border: "1px solid var(--background-modifier-border)",
  borderRadius: "12px", background: "var(--background-secondary)"
});

function field(label, tag, type, placeholder) {
  const wrapper = form.createEl("label");
  Object.assign(wrapper.style, { display: "grid", gap: "6px" });
  wrapper.createEl("span", { text: label });
  const input = wrapper.createEl(tag);
  if (type) input.type = type;
  input.placeholder = placeholder;
  input.required = true;
  input.style.width = "100%";
  input.style.boxSizing = "border-box";
  return input;
}

// The form stores a folder ID, not a path. A small settings note inside
// the destination lets it find that folder after renames, even while closed.
const source = context.file;
const markerName = "_Inbox Settings.md";
async function frontmatter(file) {
  const text = await app.vault.cachedRead(file);
  const match = text.match(/^---\r?\n([\s\S]*?)\r?\n---(?:\r?\n|$)/);
  return match ? (parseYaml(match[1]) || {}) : {};
}
let selectedId = (await frontmatter(source)).inbox_folder_id || "";
let busy = false;
let saving = false;

const setup = form.createDiv();
Object.assign(setup.style, { display: "grid", gap: "10px" });
const destinationLabel = setup.createEl("label");
destinationLabel.createEl("span", { text: "Save submissions to" });
const picker = destinationLabel.createEl("select");
picker.style.width = "100%";
picker.style.marginTop = "6px";
const createButton = setup.createEl("button", { text: "Create inbox", type: "button" });
createButton.style.justifySelf = "start";
setup.createEl("small", { text: "Choose a folder, or create an inbox for a character. Your choice is remembered for this form." });
const setupStatus = setup.createEl("div", { attr: { role: "status" } });

async function resolveFolder() {
  if (!selectedId) return null;
  const matches = [];
  for (const file of app.vault.getMarkdownFiles().filter(f => f.name === markerName)) {
    if ((await frontmatter(file)).inbox_folder_id === selectedId) matches.push(file.parent);
  }
  if (matches.length > 1) throw new Error("Two folders have the same inbox settings. Remove the copied _Inbox Settings note from the duplicate folder, then select that folder again if needed.");
  return matches[0] || null;
}
async function refresh() {
  const selected = await resolveFolder();
  picker.replaceChildren();
  picker.createEl("option", { text: "Choose a folder…", value: "" });
  const folders = app.vault.getAllLoadedFiles()
    .filter(f => f instanceof TFolder && !f.isRoot() && f.path !== "Threads" && !f.path.startsWith("Threads/") && f.path !== "_Papertrail" && !f.path.startsWith("_Papertrail/"))
    .sort((a, b) => a.path.localeCompare(b.path));
  for (const folder of folders) picker.createEl("option", { text: folder.path, value: folder.path });
  picker.value = selected?.path || "";
  setupStatus.textContent = selected ? `Saving to: ${selected.path}` :
    selectedId ? "Inbox not found. Select a folder to reconnect it." : "Choose where messages should go.";
}
async function selectFolder(folder) {
  const path = `${folder.path}/${markerName}`;
  let marker = app.vault.getAbstractFileByPath(path);
  let id;
  if (marker) {
    if (!(marker instanceof TFile)) throw new Error(`${markerName} must be a note.`);
    id = (await frontmatter(marker)).inbox_folder_id;
    if (!id || typeof id !== "string") throw new Error(`${markerName} already exists but is not an inbox settings note. Rename it before selecting this folder.`);
  } else {
    id = crypto.randomUUID();
    await app.vault.create(path, `---\n${stringifyYaml({ inbox_folder_id: id })}---\n\n# Inbox Settings\n\nThis note lets Inbox Forms follow this folder when it is renamed or moved.\nKeep this note inside the inbox and keep its filename unchanged.\n`);
  }
  await app.fileManager.processFrontMatter(source, fm => { fm.inbox_folder_id = id; });
  selectedId = id;
  await refresh();
}
async function configure(action) {
  if (busy || saving) return;
  busy = true;
  picker.disabled = createButton.disabled = true;
  try { await action(); }
  catch (error) { setupStatus.textContent = error.message || String(error); }
  finally { busy = false; picker.disabled = createButton.disabled = false; }
}
picker.addEventListener("change", () => configure(async () => {
  const folder = app.vault.getAbstractFileByPath(picker.value);
  if (!(folder instanceof TFolder)) { await refresh(); return; }
  await selectFolder(folder);
}));
class CreateInboxModal extends Modal {
  onOpen() {
    this.contentEl.createEl("h2", { text: "Create a character’s inbox" });
    const panel = this.contentEl.createEl("form");
    const label = panel.createEl("label", { text: "Character name" });
    const name = label.createEl("input", { type: "text", placeholder: "Paul" });
    name.required = true;
    name.style.width = "100%";
    const errorText = panel.createEl("p", { attr: { role: "alert" } });
    const button = panel.createEl("button", { text: "Create inbox", type: "submit", cls: "mod-cta" });
    panel.addEventListener("submit", async event => {
      event.preventDefault();
      const character = name.value.trim();
      if (!character || /[\\/:*?"<>|\u0000-\u001f]/.test(character)) {
        errorText.textContent = 'Enter a name without these characters: \\ / : * ? " < > |';
        return;
      }
      button.disabled = true;
      try {
        const path = normalizePath(`${character}'s Inbox`);
        let folder = app.vault.getAbstractFileByPath(path);
        if (!folder) folder = await app.vault.createFolder(path);
        if (!(folder instanceof TFolder)) throw new Error("A note already has that name.");
        await selectFolder(folder);
        this.close();
      } catch (error) { errorText.textContent = error.message || String(error); }
      finally { button.disabled = false; }
    });
    name.focus();
  }
  onClose() { this.contentEl.empty(); }
}
createButton.addEventListener("click", () => {
  if (!busy && !saving) new CreateInboxModal(app).open();
});
await refresh();
for (const event of ["rename", "delete", "create"]) {
  component.registerEvent(app.vault.on(event, () => {
    refresh().catch(error => { setupStatus.textContent = error.message || String(error); });
  }));
}

const email = field("Email", "input", "email", "you@example.com");
const subject = field("Subject", "input", "text", "What is this about?");
const message = field("Message", "textarea", null, "Write your message…");
message.rows = 8;
message.style.resize = "vertical";

const submit = form.createEl("button", {
  text: "Submit", type: "submit", cls: "mod-cta"
});
submit.style.justifySelf = "start";
const status = form.createEl("div", { attr: { role: "status", "aria-live": "polite" } });
status.style.fontSize = "var(--font-small)";

form.addEventListener("submit", async (event) => {
  event.preventDefault();
  if (saving || busy || !form.reportValidity()) return;
  const values = {
    email: email.value.trim(),
    subject: subject.value.trim(),
    message: message.value.trim()
  };
  if (!values.email || !values.subject || !values.message) {
    status.textContent = "Please fill in all three fields.";
    return;
  }

  saving = true;
  submit.disabled = true;
  submit.textContent = "Saving…";
  status.textContent = "";

  try {
    const target = await resolveFolder();
    if (!target) throw new Error("Choose an inbox folder above before submitting.");
    const destination = target.path;

    const now = new Date();
    const pad = (n) => String(n).padStart(2, "0");
    const date = `${now.getFullYear()}-${pad(now.getMonth() + 1)}-${pad(now.getDate())}`;
    const time = `${pad(now.getHours())}${pad(now.getMinutes())}${pad(now.getSeconds())}`;
    const title = values.subject
      .replace(/[\\/:*?"<>|#\[\]^\u0000-\u001f]/g, " ")
      .replace(/\s+/g, " ").trim().slice(0, 100).replace(/[. ]+$/g, "") || "Message";
    const base = `${destination}/${date} ${time} - ${title}`;
    const submissionId = crypto.randomUUID();
    const content = `---\n${stringifyYaml({
      papertrail_kind: "submission",
      papertrail_id: submissionId,
      current_inbox_id: selectedId,
      visited_inboxes: [selectedId],
      submitted_at: now.toISOString(),
      date_submitted: date,
      email: values.email,
      subject: values.subject
    }).trimEnd()}\n---\n\n## Original submission\n\n**From:** ${values.email}  \n**To:** ${destination}  \n**Date:** ${now.toISOString()}\n\n${values.message}\n\n<!-- papertrail-actions -->\n${controls}\n`;

    // Never overwrite an existing note, even if two forms submit at once.
    let path;
    for (let suffix = 0; ; suffix++) {
      path = `${base}${suffix ? ` (${suffix})` : ""}.md`;
      if (app.vault.getAbstractFileByPath(path)) continue;
      try {
        await app.vault.create(path, content);
        break;
      } catch (error) {
        if (!app.vault.getAbstractFileByPath(path)) throw error;
      }
    }

    email.value = subject.value = message.value = "";
    status.textContent = `Saved: ${path}`;
    new Notice(`Message saved to ${destination}.`);
  } catch (error) {
    console.error("Inbox form:", error);
    status.textContent = `Could not save: ${error.message || error}`;
    new Notice("Could not save the message. Your fields have been kept.");
  } finally {
    saving = false;
    submit.disabled = false;
    submit.textContent = "Submit";
  }
});
```
