# Daikibo Industrials — Suspected Breach Investigation
**Deloitte Cyber Job Simulation (via Forage) | Log Analysis & Incident Investigation**

> ⚠️ **Note:** This is a simulated exercise completed as part of Deloitte's Cyber Job Simulation, hosted on Forage — not a real client engagement. Daikibo Industrials is a fictional company used for training purposes. The methodology and findings below are genuine and represent my own analysis.

## Background
In this simulation, a news outlet had revealed sensitive private information about Daikibo Industrials (fictional client), and a production issue halted the client's assembly lines. The client suspected their manufacturing status dashboard had been breached. I was tasked with investigating `web_requests.log` — a record of every request made to the dashboard during the suspected attack window — to determine whether an attacker had been operating inside the system, and if so, identify the compromised account.

## Objective
1. Determine whether an internet-based attacker (no VPN access) could have directly accessed the status dashboard.
2. Analyze the web request log to identify any evidence of automated/malicious access, and isolate the affected user account.

## Methodology
Rather than scanning line by line, I approached this the way a SIEM would triage it:

1. **Establish a baseline.** Reviewed several ordinary sessions to understand normal behavior: login → dashboard page load → a handful of API calls to check factory/machine status, with irregular, human-paced gaps between requests (seconds to tens of seconds).
2. **Volume triage.** Counted total requests per source IP across all 77 IP blocks in the log. Nearly every IP fell in the 30–46 request range — consistent with a single day's normal use. One IP, `192.168.0.101`, had **138 requests**, roughly 3x the next highest.
3. **Timing analysis.** Isolated the API call timestamps for `192.168.0.101` and measured the intervals between them.
4. **Failure-mode check.** Reviewed how the session behaved once its authentication expired, to distinguish human vs. automated behavior.
5. **Brute-force check.** Searched the entire log for failed `POST /login` attempts to rule out password-guessing as the entry vector.

## Findings

**Volume anomaly:** `192.168.0.101` generated 138 requests vs. a ~35–46 norm elsewhere in the log.

**Timing anomaly:** The session began with normal, irregular human browsing (gaps of 21s, 51s, 39s, 42s, 69s), then abruptly shifted to requesting the same 4 factory-status endpoints every **exactly 3600 seconds**, on the hour, for many consecutive hours — a level of precision no human browsing session produces.

**Failure-mode anomaly:** Once the session's auth token expired (visible as a shift to `401 UNAUTHORIZED` responses), the requests continued on the identical hourly schedule rather than stopping or re-authenticating — behavior consistent with an unattended script, not a person who would notice a broken dashboard and log back in.

**Brute-force ruled out:** Of 140 total login attempts logged, **100% succeeded on the first try** — no evidence of credential guessing. This points to the attacker using an already-valid, likely stolen, credential rather than forcing their way in.

## Conclusion
The account with `authorizedUserId: mdB7yD2dp1BFZPontHBQ1Z` (associated with IP `192.168.0.101`) shows strong, multi-signal evidence of automated, non-human access: abnormal request volume, mechanically precise polling intervals, and persistence through authentication failure. Combined with the absence of any brute-force activity, this indicates the attacker used **valid but compromised employee credentials** rather than breaking the authentication system itself — meaning direct internet access to the dashboard was possible for anyone holding a stolen login, without needing VPN access to Daikibo's internal network.

## Skills Demonstrated
- Log analysis and anomaly detection
- Establishing behavioral baselines to identify outliers
- Distinguishing human vs. automated (bot) activity from timing patterns
- Incident investigation methodology (volume triage → timing analysis → failure-mode review → alternate-vector elimination)
- Clear, evidence-based security reporting

*Completed as part of Deloitte's Cyber Job Simulation on Forage.*
